---
layout: default
title: 30Yr Mortgage Interest Rates
---
<main>
  <div class="container py-5">
        <!-- Breadcrumb Navigation -->
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item"><a href="/info">Info-4-U</a></li>
        <li class="breadcrumb-item active" aria-current="page">30Yr Mortgage Interest</li>
      </ol>
    </nav>
    <!-- Intro Row with Icon -->
    <div class="row align-items-center mb-4">
      <div class="col-md-8">
        <h1>30Yr Mortgage Interest Rates</h1>
        <p class="fs-5">
          <b>US 30-Year Mortgage Rates - Weekly Updates</b><br>
          We track 30-year mortgage rates weekly to help you understand current rates and whether they're rising, falling, or staying steady. This helps you make informed decisions about home buying or refinancing.
        </p>
      </div>
      <div class="col-md-4 text-center">
        <!-- Large Bootstrap Icon -->
       <img src="/benri/benri_icon.png" alt="Benri Icon" class="img-fluid" style="max-width: 150px; height: auto;">
      </div>
    </div>
    <hr class="col-3 col-md-2 mb-5">    
    <!-- Chart Section -->
    <div class="row g-5">
      <div class="col-12">
        <!-- Latest Rate Display -->
        <div class="card bg-light border-0 mb-3">
          <div class="card-body text-center">
            <h3 class="mb-0">Latest 30Yr Mortgage Interest Rate: <span id="latest-rate" class="text-primary">Loading...</span></h3>
          </div>
        </div>  
        <div class="card shadow-sm mb-3">
          <div class="card-body">
            <canvas id="bareChart" height="140"></canvas>
          </div>
        </div>
        <p id="last-updated" class="text-center small text-muted">Loading update date…</p>
      </div>
    </div>    
    <!-- Commentary Section -->
    <div class="row g-5 mt-2">
      <div class="col-md-6">
        <h2>Commentary</h2>
        <p>You can add weekly insights or trend explanations here for readers. This section helps provide context for the data and explains what the trends mean for everyday consumers.</p>
      </div>
      <div class="col-md-6">
        <div class="card bg-light border-0">
          <div class="card-body text-center">
            <h5 class="card-title">Stay in the loop</h5>
            <p class="card-text">Sign up to get updates when this chart is refreshed.</p>
            <a href="#" class="btn btn-primary">Subscribe</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
<!-- Chart.js & data loader -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
  const SHEET_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vT5nPX2me4c9zl6MoS8lCPC1cirRMbTfU-hnAWhSX---JNatc5eEkPQPO0IYJouhmDueskUa_sX5ssa/pub?gid=1263993722&single=true&output=csv';
  fetch(SHEET_URL)
    .then(response => response.text())
    .then(csv => {
      const rows = csv.trim().split('\n').slice(1);
      const labels = [];
      const values = [];
      rows.forEach(row => {
        const [date, value] = row.split(',');
        labels.push(date);
        values.push(parseFloat(value));
      });
      // Display latest rate
      const latestRate = values[values.length - 1];
      document.getElementById("latest-rate").textContent = `${latestRate.toFixed(2)}%`;
      document.getElementById("last-updated").textContent = `Last updated: ${labels[labels.length - 1]}`;
      const ctx = document.getElementById('bareChart').getContext('2d');
      new Chart(ctx, {
        type: 'line',
        data: {
          labels: labels,
          datasets: [{
            label: '30-Year Mortgage Rate',
            data: values,
            borderColor: '#0d6efd',
            backgroundColor: 'rgba(13, 110, 253, 0.1)',
            borderWidth: 2,
            pointRadius: 2,
            fill: true,
            tension: 0.3
          }]
        },
        options: {
          responsive: true,
          scales: {
            y: {
              beginAtZero: false,
              suggestedMin: Math.min(...values) - 0.5,
              title: {
                display: true,
                text: 'Interest Rate (%)'
              }
            },
            x: {
              title: {
                display: true,
                text: 'Date'
              }
            }
          },
          plugins: {
            legend: { display: false },
            tooltip: {
              callbacks: {
                label: context => `${context.parsed.y.toFixed(2)}%`
              }
            }
          }
        }
      });
    })
    .catch(err => {
      document.getElementById("last-updated").textContent = "Error loading data.";
      console.error('Error fetching sheet:', err);
    });
</script>
