<template>
    <div class="flex items-center justify-center mb-4 mt-20">
        <input type="file" id="fileInput" accept=".xlsx, .csv" class="hidden" @change="uploadFile" />
        <label
            for="fileInput"
            @click="importFile"
            :class="{
                'cursor-not-allowed': loading,
                'opacity-50': loading,
            }"
            class="py-3 px-6 border border-green-500 rounded-md cursor-pointer bg-gradient-to-r from-green-400 to-green-600 hover:from-green-600 hover:to-green-800 transition duration-300 ease-in-out outline-none text-white font-extrabold text-2xl"
        >
            {{ loading ? "Loading file..." : "Import .xlsx or .csv data" }}
        </label>
    </div>

    <div
        v-if="uploadedMessage"
        class="text-center p-4 mb-4 text-lg text-green-800 rounded-lg bg-green-50 dark:bg-gray-800 dark:text-green-400"
        role="alert"
    >
        <p class="font-extrabold">{{ uploadedMessage }}</p>
    </div>

    <div
        v-if="errorMessage"
        class="text-center p-4 mb-4 text-lg text-red-800 rounded-lg bg-red-50 dark:bg-gray-800 dark:text-red-400"
        role="alert"
    >
        <p class="font-extrabold">{{ errorMessage }}</p>
    </div>

    <h2
        class="mt-10 mb-10 text-4xl font-semibold text-center bg-gradient-to-r from-blue-500 to-green-500 text-transparent bg-clip-text"
    >
        Monthly Recurring Revenue
    </h2>

    <Bar
        v-if="chartDataMRR && chartDataMRR.labels && chartDataMRR.datasets"
        :options="chartOptionsMRR"
        :data="chartDataMRR"
    />

    <h2
        class="mt-20 mb-10 text-4xl font-semibold text-center bg-gradient-to-r from-orange-500 to-purple-500 text-transparent bg-clip-text"
    >
        Monthly Churn Rate
    </h2>

    <Bar
        v-if="chartDataChurn && chartDataChurn.labels && chartDataChurn.datasets"
        :options="chartOptionsChurn"
        :data="chartDataChurn"
    />
</template>

<script>
import { onMounted, ref } from "vue";
import { initFlowbite } from "flowbite";
import { Bar } from "vue-chartjs";
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from "chart.js";

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

export default {
    name: "BarChart",
    components: { Bar },
    setup() {
        onMounted(() => {
            initFlowbite();
        });

        const loading = ref(false);
        const uploadedMessage = ref("");
        const errorMessage = ref("");

        const initialChartDataMRR = ref({
            labels: [],
            datasets: [{ data: [] }],
        });

        const initialChartDataChurn = ref({
            labels: [],
            datasets: [{ data: [] }],
        });

        const initialChartOptionsMRR = ref({
            responsive: true,
            scales: {
                y: {
                    ticks: {
                        callback: function (value, index, values) {
                            return `${value.toLocaleString("pt-BR", {
                                style: "currency",
                                currency: "BRL",
                                minimumFractionDigits: 2,
                                maximumFractionDigits: 2,
                            })}`;
                        },
                    },
                },
            },
        });

        const initialChartOptionsChurn = ref({
            responsive: true,
            scales: {
                y: {
                    ticks: {
                        callback: function (value, index, values) {
                            return `${value.toFixed(2)}%`;
                        },
                    },
                },
            },
        });

        const generateGradientColors = (count) => {
            const colors = [];
            for (let i = 0; i < count; i++) {
                const hue = (i * 360) / count;
                colors.push(`hsl(${hue}, 70%, 50%)`);
            }
            return colors;
        };

        const uploadFile = async (event) => {
            loading.value = true;

            const file = event.target.files[0];
            const formData = new FormData();
            formData.append("file", file);

            try {
                const response = await fetch(`${import.meta.env.VITE_DNS_MICROSAAS_API}/import-file`, {
                    method: "POST",
                    body: formData,
                });

                if (response.ok) {
                    const responseData = await response.json();

                    initialChartDataMRR.value = {
                        labels: Object.keys(responseData.data.mrr),
                        datasets: [
                            {
                                label: "Monthly Recurring Revenue",
                                data: Object.values(responseData.data.mrr),
                                backgroundColor: generateGradientColors(Math.floor(Math.random() * 20) + 1),
                                borderWidth: 1,
                                fill: false,
                            },
                        ],
                    };

                    initialChartDataChurn.value = {
                        labels: Object.keys(responseData.data.churnRate),
                        datasets: [
                            {
                                label: "Churn Rate",
                                data: Object.values(responseData.data.churnRate),
                                backgroundColor: "red",
                                borderWidth: 1,
                                fill: false,
                            },
                        ],
                    };

                    errorMessage.value = "";
                    uploadedMessage.value = "Charts Data Updated!";
                } else {
                    uploadedMessage.value = "";
                    errorMessage.value =
                        "File upload failed. Please verify if is a .xlsx or .csv file with correct data";
                }
            } catch (error) {
                uploadedMessage.value = "";
                errorMessage.value = "File upload failed. Please verify if is a .xlsx or .csv file with correct data";
            } finally {
                loading.value = false;
            }
        };

        return {
            chartDataMRR: initialChartDataMRR,
            chartDataChurn: initialChartDataChurn,
            chartOptionsMRR: initialChartOptionsMRR,
            chartOptionsChurn: initialChartOptionsChurn,
            uploadFile,
            loading,
            errorMessage,
            uploadedMessage,
        };
    },
};
</script>
