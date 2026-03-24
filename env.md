# Using .env files to manage base path

In projects with multiple contributors, we can use a `.env` file to keep local paths private (i.e. ignored by git) but easy to set up across users.

Given the following folder structure:

```bash
project_root/
│
├── .env.example         ← committed to repo
├── .env                 ← NOT committed (ignored)
├── .gitignore           ← must contain .env but not .env.example
├── src/
│   └── config.py        ← handles env/config loading
└── notebooks/
    └── 0_data_exploration.ipynb
```

Create a copy of the `.env.example` file and update it to point to your local path containing the relevant data. Make sure `.env` is listed in `.gitignore`.

```ini
# Copy this file to `.env` and adjust paths locally

# Base folder for local data (update this for your machine)
DATA_PATH=C:\Users\<your_user>\path\to\data
```
