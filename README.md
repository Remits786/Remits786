- name: 🚀 Auto Deploy to Hostinger VPS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy via SSH
    runs-on: ubuntu-latest

    steps:
      - name: 📂 SSH to Server & Pull Latest Code
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_IP }}
          username: ${{ secrets.USERNAME }}
          key: ${{ secrets.SSH_KEY }}
          script: |
            cd /var/www/eremit
            git pull origin main
            cd backend
            npm install
            pm2 restart eremit-api
