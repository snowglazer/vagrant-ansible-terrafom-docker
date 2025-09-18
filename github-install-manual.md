Got it 👍 — right now your playbook **automates** installing and configuring a GitHub Actions runner using Ansible.
If you want to do it **manually (step by step)** without Ansible, here’s the equivalent procedure you’d run on your VM (as `vagrant` user):

---

### ⚙️ Manual Steps to Install GitHub Actions Runner

1. **Install dependencies**

   ```bash
   sudo apt update
   sudo apt install -y curl tar jq
   ```

2. **Create a runner directory**

   ```bash
   sudo mkdir -p /opt/actions-runner
   sudo chown vagrant:vagrant /opt/actions-runner
   cd /opt/actions-runner
   ```

3. **Download the runner**

   ```bash
   curl -o actions-runner-linux-x64-2.328.0.tar.gz -L \
   https://github.com/actions/runner/releases/download/v2.328.0/actions-runner-linux-x64-2.328.0.tar.gz
   ```

4. **Extract the archive**

   ```bash
   tar xzf ./actions-runner-linux-x64-2.328.0.tar.gz
   ```

5. **Get a registration token from GitHub**

   * Go to your repository:
     `https://github.com/<your-org-or-user>/<your-repo>/settings/actions/runners/new`
   * Copy the **registration token** shown there.

   *(In your playbook this was automated with the GitHub API and `github_pat`, but for manual setup you fetch it via the GitHub UI).*

6. **Configure the runner**

   ```bash
   ./config.sh --url https://github.com/<your-org-or-user>/<your-repo> \
   --token <your_registration_token> --unattended
   ```

7. **Install the runner as a service**

   ```bash
   sudo ./svc.sh install
   ```

8. **Start the runner service**

   ```bash
   sudo ./svc.sh start
   ```

9. **Verify it’s running**

   ```bash
   sudo ./svc.sh status
   ```

   Or check in your GitHub repo → **Settings → Actions → Runners**.

---

👉 Do you want me to also give you the **Windows manual steps** (since you used Git Bash + Vagrant), or only Linux steps for inside the VM?
