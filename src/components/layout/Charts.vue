<template>
	<div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
		<!-- Animated Revenue Line Chart -->
		 <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md
		 dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20">
				<h2 class="text-lg font-semibold mb-4">Monthly Revenue</h2>
				<Line :data="revenueChartData" :options="lineChartOptions" class="max-h-[300px]" :key="lineChartKey"/>
		 </div>

		 <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md
		 dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20">
		 	<h2 class="text-lg font-semibold mb-4">Revenue Source</h2>
			<Doughnut :data="doughnutChartData" :options="doughnutChartOptions" class="max-h-[300px]" :key="doughnutChartKey"/>
		</div>
	</div>	
</template>
<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { Doughnut, Line } from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement,
  type ChartOptions,
  type ChartData
} from 'chart.js';

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement
);


type LineChartData = ChartData<'line', number[], string>;
type DoughnutChartData = ChartData<'doughnut', number[], string>;
type LineChartOptions = ChartOptions<'line'>;
type DoughnutChartOptions = ChartOptions<'doughnut'>;


const lineChartKey = ref<number>(0);
const doughnutChartKey = ref<number>(0);

onMounted(() => {
  lineChartKey.value++;
  doughnutChartKey.value++;
});


const revenueChartData = ref<LineChartData>({
  labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
  datasets: [{
    label: 'Revenue ($)',
    data: [1200, 1900, 3000, 5000, 20000, 3000],
    fill: false,
    borderColor: '#E82561',
    backgroundColor: '#E82561',
    tension: 0.4,
  }]
});

const lineChartOptions = ref<LineChartOptions>({
  responsive: true,
  maintainAspectRatio: false,
  animations: {
    tension: {
      duration: 1000,
      easing: 'linear',
      from: 1,
      to: 0,
      loop: false
    }
  },
  plugins: {
    legend: {
      labels: {
        color: '#64748B',
      }
    }
  },
  scales: {
    x: {
      grid: {
        color: 'rgba(0,0,0,0.1)',
      },
      ticks: {
        color: '#64748B',
      }
    },
    y: {
      grid: {
        color: 'rgba(0,0,0,0.1)',
      },
      ticks: {
        color: '#64748B',
      }
    }
  }
});


const doughnutChartData = ref<DoughnutChartData>({
  labels: ['Products', 'Services', 'Subscription', 'Consulting'],
  datasets: [{
    data: [35, 25, 20, 20],
    backgroundColor: ['#4635B1', '#E82561', '#ECE852', '#FFA24C'],
    borderWidth: 0,
    hoverOffset: 10,
  }]
});

const doughnutChartOptions = ref<DoughnutChartOptions>({
  responsive: true,
  maintainAspectRatio: false,
  cutout: '70%',
  animations: {
    animateRotate: {
      duration: 1000,
      easing: 'easeOutQuad'
    },
    animateScale: {
      duration: 1000,
      easing: 'easeOutQuad'
    }
  },
  plugins: {
    legend: {
      position: 'right',
      labels: {
        color: '#64748B',
        boxWidth: 12,
        padding: 16,
      }
    },
    tooltip: {
      callbacks: {
        label: (context) => {
          return `${context.label}: ${context.formattedValue}%`;
        }
      }
    }
  }
});
</script>