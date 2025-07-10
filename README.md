Your App Name
Description of your app...

Quick Install to Reachy
<div style="border: 1px solid #ddd; padding: 20px; border-radius: 8px; margin: 20px 0; background: #f9f9f9;"> <h3>🤖 Install to Your Reachy Dashboard</h3> <p>Enter your Reachy dashboard URL to install this app directly:</p> <div style="margin: 15px 0;"> <label for="dashboardUrl" style="display: block; margin-bottom: 5px;">Dashboard URL:</label> <input type="url" id="dashboardUrl" value="http://localhost:8000" placeholder="http://your-reachy-ip:8000" style="width: 100%; max-width: 300px; padding: 8px; border: 1px solid #ccc; border-radius: 4px;" /> </div>
<button id="installBtn" onclick="installToReachy()" style="background: 
#0066cc; color: white; padding: 10px 20px; border: none; border-radius: 4px; cursor: pointer; font-size: 16px;"> 📥 Install to Reachy </button>

<div id="installStatus" style="margin-top: 10px; padding: 10px; display: none; border-radius: 4px;"></div> </div> <script> function getCurrentRepoUrl() { // Get current GitHub repository URL const currentUrl = window.location.href; // Convert GitHub URL to raw content URL or keep as is depending on your needs return currentUrl.replace(/\/$/, ''); } async function installToReachy() { const dashboardUrl = document.getElementById('dashboardUrl').value.trim(); const statusDiv = document.getElementById('installStatus'); const installBtn = document.getElementById('installBtn'); if (!dashboardUrl) { showStatus('error', 'Please enter your Reachy dashboard URL'); return; } try { installBtn.disabled = true; installBtn.innerHTML = '⏳ Installing...'; showStatus('loading', 'Connecting to your Reachy dashboard...'); // Test connection const testResponse = await fetch(`${dashboardUrl}/api/status`, { method: 'GET', mode: 'cors', }); if (!testResponse.ok) { throw new Error('Cannot connect to dashboard. Make sure the URL is correct and the dashboard is running.'); } showStatus('loading', 'Starting installation...'); // Get current repo URL const repoUrl = getCurrentRepoUrl(); // Extract app name from repository name or pyproject.toml const appName = extractAppName(repoUrl); // Start installation const installResponse = await fetch(`${dashboardUrl}/api/install`, { method: 'POST', mode: 'cors', headers: { 'Content-Type': 'application/json', }, body: JSON.stringify({ url: repoUrl, name: appName }) }); const result = await installResponse.json(); if (installResponse.ok) { showStatus('success', `✅ Installation started for "${appName}"! Check your dashboard for progress.`); } else { throw new Error(result.detail || 'Installation failed'); } } catch (error) { console.error('Installation error:', error); showStatus('error', `❌ ${error.message}`); } finally { installBtn.disabled = false; installBtn.innerHTML = '📥 Install to Reachy'; } } function extractAppName(repoUrl) { const parts = repoUrl.split('/'); const repoName = parts[parts.length - 1]; return repoName.toLowerCase().replace(/[^a-z0-9-_]/g, '-'); } function showStatus(type, message) { const statusDiv = document.getElementById('installStatus'); const colors = { success: '#d4edda', error: '#f8d7da', loading: '#d1ecf1' }; statusDiv.style.display = 'block'; statusDiv.style.backgroundColor = colors[type] || '#f8f9fa'; statusDiv.style.border = `1px solid ${colors[type] || '#dee2e6'}`; statusDiv.textContent = message; } </script>
Manual Installation
If the button doesn't work, you can manually install by:

Open your Reachy dashboard at http://your-reachy-ip:8000
Navigate to the Apps section
Use "Install from URL" with: https://github.com/your-username/your-repo
Features
Feature 1
Feature 2
Feature 3
