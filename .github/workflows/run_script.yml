name: Run Python script every 30 minutes

on:
  schedule:
    - cron: '*/30 * * * *'

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.13.2'  # Specify the Python version you need

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install requests

    - name: Run Python script
      run: python BodhAi/question_respone.py
