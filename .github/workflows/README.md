# Step to Reproduce

git clone https://github.com/ARINC-IA/CSMIM.git
cd CSMIM
git checkout test-pr40-duplicate-warning        # has the scripts + test fixture

python3 -m venv .venv
.venv/bin/pip install -r .github/workflows/requirements.txt yamllint

### 1. schema/structure tests
.venv/bin/pytest .github/workflows/test-csmim-syntax.py -v

### 2. yaml lint
.venv/bin/yamllint -c .yamllint -s types

### 3. duplicate warnings (exactly as CI runs it on a PR)
.venv/bin/python .github/workflows/warn-duplicates.py --base origin/main
