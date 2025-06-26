---
layout: default
title: Welcome to Benri
---

<style>
  .tool-item {
    transition: all 0.2s ease;
    border-left: 3px solid transparent;
  }
  
  .tool-item:hover {
    border-left-color: var(--bs-primary);
    transform: translateX(5px);
  }
  
  .coming-soon-item {
    opacity: 0.7;
    cursor: default;
  }
  
  .coming-soon-item:hover {
    transform: none;
    border-left-color: transparent;
  }
</style>

<div class="text-center py-5">
  <h1 class="display-4 fw-bold">Welcome to Benri</h1>
  <p class="lead text-muted">Building simple, helpful tools for everyone. All free, no <i>catch</i>.</p>
</div>

<div class="container">
  <div class="row">
    <div class="col-lg-8 mx-auto">
      <p class="text-muted mb-4">Here you'll find small but helpful tools to make your life a little easier. Track mortgage rates, remember important dates, and get timely reminders for the things that matter - all completely free. Built and incorporating AI for ease of use.</p>
       <!-- Email Signup -->
      <div class="bg-light border rounded p-4 my-4">
        <h6 class="fw-semibold mb-2">Get notified when we launch new tools</h6>
        <p class="text-muted small mb-3">We'll only email you about new tools. No spam, ever.</p>
        <div class="d-flex flex-column flex-md-row gap-2" style="max-width: 400px;">
          <input type="email" class="form-control form-control-sm" placeholder="Enter your email" id="emailSignup">
          <button class="btn btn-primary btn-sm" type="button" id="signupBtn">Notify Me</button>
        </div>
        <small class="text-muted">Join our community of productivity enthusiasts.</small>
      </div>
      <!-- Financial Tools -->
      <h5 class="fw-semibold mt-4 mb-3 pb-2 border-bottom">💰 Financial Tools</h5>    
      <div class="list-group list-group-flush">
        <a href="/benri/bare.html" class="list-group-item list-group-item-action tool-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">🧺</span>
              <div>
                <div class="fw-medium">Bare Necessities Chart</div>
                <small class="text-muted">Index tracking the main household goods and essential items pricing trends</small>
              </div>
            </div>
            <span class="badge bg-primary-subtle text-primary-emphasis rounded-pill">Live</span>
          </div>
        </a>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">📈</span>
              <div>
                <div class="fw-medium">Mortgage Rate Tracker</div>
                <small class="text-muted">Real-time mortgage rate monitoring with historical trends and predictions</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">💰</span>
              <div>
                <div class="fw-medium">Budget Planner</div>
                <small class="text-muted">Smart budget planning with AI-powered insights and spending analysis</small>
              </div>
            </div>
            <span class="badge bg-warning-subtle text-warning-emphasis rounded-pill">Beta</span>
          </div>
        </div>
      </div?
      <!-- Productivity Tools -->
      <h5 class="fw-semibold mt-4 mb-3 pb-2 border-bottom">⚡ Productivity Tools</h5>
      <div class="list-group list-group-flush">
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">📅</span>
              <div>
                <div class="fw-medium">Date Reminder</div>
                <small class="text-muted">Never forget important dates with smart reminders and notifications</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">⏰</span>
              <div>
                <div class="fw-medium">Task Timer</div>
                <small class="text-muted">Pomodoro technique timer with productivity tracking and analytics</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">📝</span>
              <div>
                <div class="fw-medium">Quick Notes</div>
                <small class="text-muted">Lightning-fast note taking with AI-powered organization and search</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
      </div>
      <!-- Utilities -->
      <h5 class="fw-semibold mt-4 mb-3 pb-2 border-bottom">🔧 Utilities</h5>
      <div class="list-group list-group-flush">
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">🔧</span>
              <div>
                <div class="fw-medium">Unit Converter</div>
                <small class="text-muted">Convert between different units of measurement with precision and ease</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">🎨</span>
              <div>
                <div class="fw-medium">Color Palette Generator</div>
                <small class="text-muted">Generate beautiful color palettes for your design projects</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
        <div class="list-group-item tool-item coming-soon-item p-3">
          <div class="d-flex justify-content-between align-items-start">
            <div class="d-flex">
              <span class="me-3 fs-5">📊</span>
              <div>
                <div class="fw-medium">QR Code Generator</div>
                <small class="text-muted">Create custom QR codes for URLs, text, and contact information</small>
              </div>
            </div>
            <span class="badge bg-secondary-subtle text-secondary-emphasis rounded-pill">Coming Soon</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
document.getElementById('signupBtn').addEventListener('click', function() {
    const email = document.getElementById('emailSignup').value;
    if (email && email.includes('@')) {
        alert('Thanks for signing up! We\'ll notify you when new tools are available.');
        document.getElementById('emailSignup').value = '';
    } else {
        alert('Please enter a valid email address.');
    }
});
</script>
