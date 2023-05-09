name: Continuous Dependency Updating

on:
  schedule:
    - cron: '0 0 * * *' # Run daily at 00:00 UTC
  workflow_dispatch: # Allows manual triggering of the workflow

jobs:
  update_dependencies:
    runs-on: ubuntu-latest

    steps:
    - name: Check out repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.9

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Update dependencies
      run: |
        pip install --upgrade --upgrade-strategy eager

    - name: Save updated requirements
      run: |
        pip freeze > requirements.txt

    - name: Run tests
      run: |
        pip install pytest
        pytest

    - name: Commit and push changes
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"
        git add requirements.txt
        git commit -m "Update dependencies via CDU" || exit 0
        git push
