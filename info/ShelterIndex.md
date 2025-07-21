<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shelter Rates</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <main>
        <div class="container py-5">
            <!-- Breadcrumb Navigation -->
            <nav aria-label="breadcrumb">
                <ol class="breadcrumb">
                    <li class="breadcrumb-item"><a href="/">Home</a></li>
                    <li class="breadcrumb-item"><a href="/info">Info-4-U</a></li>
                    <li class="breadcrumb-item active" aria-current="page">Shelter Rates</li>
                </ol>
            </nav>
            <!-- Intro Row with Icon -->
            <div class="row align-items-center mb-4">
                <div class="col-md-8">
                    <h1>Shelter Rates</h1>
                    <p class="fs-5">
                        <b>US Shelter Rates - Weekly Updates</b><br>
                        We track shelter rates weekly to help you understand current rates and whether they're rising, falling, or staying steady. This helps you make informed decisions about housing costs and market trends.
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
                            <h3 class="mb-0">Latest Shelter Rate: <span id="latest-rate" class="text-primary">Loading...</span></h3>
                        </div>
                    </div>
                    <p id="last-updated" class="text-center small text-muted mb-4">Loading update date…</p>
                    <!-- Year Selector -->
                    <div class="card mb-3">
                        <div class="card-body">
                            <div class="row align-items-center">
                                <div class="col-md-6">
                                    <label for="yearSelect" class="form-label"><strong>View data starting from:</strong></label>
                                </div>
                                <div class="col-md-6">
                                    <select class="form-select" id="yearSelect">
                                        <!-- Options will be populated by JavaScript -->
                                    </select>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="card shadow-sm mb-3">
                        <div class="card-body">
                            <canvas id="bareChart" height="140"></canvas>
                        </div>
                    </div>
                </div>
            </div>   
            <!-- Commentary Section -->
            <div class="row g-5 mt-2">
                <div class="col-md-6">
                    <h2>Commentary</h2>
                    <p>You can add weekly insights or trend explanations here for readers. This section helps provide context for the data and explains what the trends mean for everyday consumers regarding shelter costs and housing market conditions.</p>
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
        const SHEET_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRWBdWUYQ4N2leMbg1PxjaIj219v4nQ3gb_TwGhO45XsTK04cyYO-vHF8rjC20G1p-R_k0wRfh13TQE/pub?gid=143034316&single=true&output=csv';
        let allData = [];
        let chart = null;
        function parseDate(dateStr) {
            // Handle different date formats that might come from the spreadsheet
            const date = new Date(dateStr);
            return date;
        }
        function filterDataByYear(startYear) {
            return allData.filter(item => {
                const itemYear = parseDate(item.date).getFullYear();
                return itemYear >= startYear;
            });
        }
        function updateChart(startYear) {
            const filteredData = filterDataByYear(startYear);
            const labels = filteredData.map(item => item.date);
            const values = filteredData.map(item => item.value);
            
            chart.data.labels = labels;
            chart.data.datasets[0].data = values;
            chart.options.scales.y.suggestedMin = Math.min(...values) - 0.5;
            chart.update();
        }
        function populateYearSelector() {
            const yearSelect = document.getElementById('yearSelect');
            const earliestYear = Math.min(...allData.map(item => parseDate(item.date).getFullYear()));
            const currentYear = new Date().getFullYear();            
            // Clear existing options
            yearSelect.innerHTML = '';            
            // Add year options from current year down to earliest year
            for (let year = currentYear; year >= earliestYear; year--) {
                const option = document.createElement('option');
                option.value = year;
                option.textContent = year;
                if (year === 2020) {
                    option.selected = true; // Default to 2020
                }
                yearSelect.appendChild(option);
            }     
            // Add event listener for year changes
            yearSelect.addEventListener('change', function() {
                updateChart(parseInt(this.value));
            });
        }
        fetch(SHEET_URL)
            .then(response => response.text())
            .then(csv => {
                const rows = csv.trim().split('\n');
                const headers = rows[0].split(',');
                
                // Find the Shelter column index
                const shelterIndex = headers.findIndex(header => header.toLowerCase().includes('shelter'));
                if (shelterIndex === -1) {
                    throw new Error('Shelter column not found');
                }
                
                // Assuming first column is date
                const dataRows = rows.slice(1);
                
                // Store all data
                allData = dataRows.map(row => {
                    const columns = row.split(',');
                    const date = columns[0];
                    const shelterValue = parseFloat(columns[shelterIndex]);
                    
                    return {
                        date: date,
                        value: shelterValue
                    };
                }).filter(item => !isNaN(item.value)); // Filter out invalid values
                
                // Display latest rate
                const latestRate = allData[allData.length - 1].value;
                document.getElementById("latest-rate").textContent = `${latestRate.toFixed(2)}`;
                document.getElementById("last-updated").textContent = `Last updated: ${allData[allData.length - 1].date}`;
                
                // Populate year selector
                populateYearSelector();
                
                // Filter data to start from 2020 by default
                const defaultData = filterDataByYear(2020);
                const labels = defaultData.map(item => item.date);
                const values = defaultData.map(item => item.value);
                
                // Create chart
                const ctx = document.getElementById('bareChart').getContext('2d');
                chart = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: labels,
                        datasets: [{
                            label: 'Shelter Rate',
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
                                    text: 'Shelter Rate'
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
                                    label: context => `${context.parsed.y.toFixed(2)}`
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
</body>
</html>
