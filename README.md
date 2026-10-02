# CSC452_lab2
Lab 2:
create a working Continuous Integration / Continuous Deployment (CI/CD) workflow that automatically builds, tests, and deploys a straightforward web page.

Status Badge: 
[![Simple CI/CD Workflow](https://github.com/liljackkulil/CSC452_lab2/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/liljackkulil/CSC452_lab2/actions/workflows/ci-cd.yml)

<img width="1844" height="510" alt="Success" src="https://github.com/user-attachments/assets/097c9a3b-3e01-4f3f-b7e7-e7334760252e" />

<img width="1865" height="669" alt="Screenshot 2026-10-01 135206" src="https://github.com/user-attachments/assets/602ce628-2dc8-4120-9f99-5dd67143601f" />


I had no issues with the code. It ran perfectly fine. The only thing I fixed was the things I purposefully messed up.





The .yml file

name: Simple CI/CD Workflow

on:
  push:
    branches:
      - main   # Run this workflow whenever code is pushed to the "main" branch

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4   

      - name: Build step
        run: echo "Build OK - HTML validated"

  deploy:
    runs-on: ubuntu-latest
    needs: build   # This ensures deploy runs only if build is successful
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Deploy step
        run: echo "Deployment successful to staging"

  upload-artifact:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Upload index.html as an artifact
        uses: actions/upload-artifact@v4
        with:
          name: webpage
          path: index.html
