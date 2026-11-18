# Creation and Maintenance of Virtual Environment

1. **Create a Virtual Environment (With Specific Version Support):** Isolate your project dependencies.
Isolate your project from the global system Python. To use a specific version (such as Python 3.12), explicitly call that version's interpreter:

```bash
python3.12 -m venv venv

```

*(Or use `python3 -m venv venv` for your default system version).*


2. **Activate the Virtual Environment:** Target your isolated workspace.
Turn on the virtual environment so your terminal sessions use this isolated space:

```bash
source venv/bin/activate

```

*Verification:* Your terminal prompt will show `(venv)` at the beginning of the line.


3. **Install Production Dependencies:** Using requirements.txt.
Install the core packages required for your application to run live in production:

```bash
pip install -r requirements.txt

```


4. **Install Development Tools:** Using requirements-dev.txt.
Layer on testing and debugging tools (like `pytest` and `httpx`) that you only need while writing code. Your `requirements-dev.txt` should include `-r requirements.txt` at the top, then install with:

```bash
pip install -r requirements-dev.txt

```


5. **Keep Dependencies Up to Date:** Using pip freeze.
If you install packages on the fly during development, automatically capture your environment's exact current packages and versions to update your file:

```bash
pip freeze > requirements.txt

```


---

### Why This Workflow Powers Collaboration and Deployment

* **Eliminates "It Works on My Machine":** By pinning exact package versions (e.g., using `==`) and capturing them via `pip freeze`, every team member runs an identical codebase environment, preventing sudden version-mismatch bugs.
* **Seamless Team Collaboration:** Tracking both `requirements.txt` and `requirements-dev.txt` in Git means developers can effortlessly sync production setups and development testing suites with a single command.
* **Reliable Cloud Deployment:** Cloud hosting platforms and Docker containers look directly for `requirements.txt` to build your production environment. Because versions are locked and precise, you avoid unexpected deployment failures caused by upstream library updates.◊