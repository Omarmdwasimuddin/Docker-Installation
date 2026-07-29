## Docker Desktop Windows Installation Guide

## ধাপ ১: Docker Desktop Installer Download ও Install

#### ১. Download link: [Docker Desktop for Windows (x86_64)](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)
#### ২. `.exe` ফাইলে double-click করো
#### ৩. Installer দুইটা option দেবে:
   - **Per-user** (recommended) — admin লাগবে না, `%LOCALAPPDATA%\Programs\DockerDesktop`-এ install হবে
   - **All users** — admin লাগবে
#### ৪. Configuration page-এ **"Use WSL 2 instead of Hyper-V"** checked আছে কিনা দেখে নাও (ঠিক আছে, এটা default)
#### ৫. Wizard অনুসরণ করে install সম্পূর্ণ করো

### Command Line দিয়ে Install (বিকল্প)
```console
"Docker Desktop Installer.exe" install --user
```

> Modern Windows (10 version 2004+ / Windows 11)-এ WSL2 backend সাধারণত installer নিজেই handle করে দেয়। তাই বেশিরভাগ ক্ষেত্রে আলাদা করে WSL manually enable করার দরকার হয় না — সরাসরি এই ধাপ থেকেই শুরু করো।

---

## ধাপ ২: Docker Desktop চালু করা

- Start menu থেকে "Docker Desktop" search করে ওপেন করো
- প্রথমবার ওপেন করলে Docker Subscription Service Agreement দেখাবে — **Accept** দিতে হবে (personal/non-commercial use ফ্রি)
- Docker whale icon (🐳) taskbar-এ দেখা গেলে বুঝবে Docker running

---

## ধাপ ৩: Install Verify করা

CMD/PowerShell-এ:
```console
docker --version
docker run hello-world
```
`hello-world` container successfully run হলে বুঝবে সব ঠিক আছে।

---

## Fallback: WSL2 সংক্রান্ত Error দিলে (শুধু প্রয়োজন হলে)

ধাপ ১-এ Docker installer/open করার সময় যদি এই ধরনের error দেখায় —
- "WSL 2 installation is incomplete"
- "WSL kernel update required"
- "WSL 2 is not installed"

তাহলে নিচের steps follow করো:

PowerShell বা CMD **Administrator হিসেবে** ওপেন করে:
```powershell
wsl --install
```
এই command WSL feature চালু করে, এবং default Linux distro (Ubuntu) install করে দেয়। Restart চাইবে — restart করে দাও।

আগে থেকেই WSL থাকলে শুধু update করো:
```powershell
wsl --update
```

Version চেক করতে:
```powershell
wsl --version
```
> Docker Desktop-এর জন্য WSL version ২.১.৫ বা তার উপরে লাগবে।

Restart-এর পর আবার ধাপ ১-এ ফিরে গিয়ে Docker Desktop installer চালাও — এবার আর error আসার কথা না।

**Check করতে চাও WSL আগে থেকে ready কিনা?** Installer চালানোর আগেই এই command run করে দেখতে পারো:
```powershell
wsl --status
```
Output normally আসলে বুঝবে WSL already configured — Fallback section skip করে সরাসরি ধাপ ১ থেকে শুরু করতে পারো।

---

## Note: RAM Optimization

তোমার RAM ৮GB — এটা minimum requirement ঠিক ঠিক পূরণ করে, কিন্তু Docker চালানোর সময় যদি একাধিক heavy container run করো তাহলে system slow লাগতে পারে, কারণ WSL2 নিজেই কিছু RAM eat করে।

ভালো হয় `.wslconfig` ফাইল দিয়ে WSL2-এর memory usage limit set করে রাখলে:
```
[wsl2]
memory=4GB
```
File location: `%USERPROFILE%\.wslconfig`

এটা করলে WSL2 সর্বোচ্চ 4GB use করবে, বাকি RAM Windows-এর অন্য কাজের জন্য free থাকবে।

---

## Reference
Official docs: https://docs.docker.com/desktop/setup/install/windows-install/
