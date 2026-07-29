## Docker Desktop Windows Installation Guide

**PC Info:** Intel Core i5-10400 @ 2.90GHz | 8GB RAM | 64-bit OS, x64-based processor

Ei PC WSL2 backend er minimum requirement thik thik pura kore (SLAT support ache, 64-bit, 8GB RAM).

---

## Step 1: WSL 2 Enable + Update Kora

PowerShell ba CMD **Administrator hisebe** open kore:

```powershell
wsl --install
```

Ei command WSL feature on kore, ar default Linux distro (Ubuntu) install kore dey. Restart magbe — restart kore dao.

Already WSL thakle just update koro:

```powershell
wsl --update
```

Version check korte:

```powershell
wsl --version
```

> Docker Desktop er jonno WSL version 2.1.5 ba tar upore lagbe.

---

## Step 2: Hardware Virtualization On Kora (BIOS/UEFI)

Ei ta khub important — na thakle Docker chalbe na:

1. PC restart kore BIOS/UEFI e jao (usually `Del` / `F2` / `F10` key — motherboard bhede alada hoy)
2. **Intel VT-x** ba **Virtualization Technology** option khuje on koro
3. Save kore exit koro

Windows e already on ache kina check korte: **Task Manager > Performance tab > CPU** e "Virtualization: Enabled" lekha thakle beshi kichu korte hobe na.

---

## Step 3: Docker Desktop Installer Download + Install

1. Download link: [Docker Desktop for Windows (x86_64)](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)
2. `.exe` file e double-click koro
3. Installer duita option debe:
   - **Per-user** (recommended) — admin lagbe na, `%LOCALAPPDATA%\Programs\DockerDesktop` e install hobe
   - **All users** — admin lagbe
   
   Tumi সাধারণত **per-user** option nile shohoj hobe.
4. Configuration page e **"Use WSL 2 instead of Hyper-V"** checked ache kina dekhe nao (thik ache, ei ta default)
5. Wizard follow kore install complete koro

### Command Line diye Install (alternative)

```console
"Docker Desktop Installer.exe" install --user
```

---

## Step 4: Docker Desktop Start Kora

- Start menu theke "Docker Desktop" search kore open koro
- Prothom bar open korle Docker Subscription Service Agreement dekhabe — **Accept** dite hobe (personal/non-commercial use free)
- Docker whale icon (🐳) taskbar e dekha gele bujbe Docker running

---

## Step 5: Verify Install

CMD/PowerShell e:

```console
docker --version
docker run hello-world
```

`hello-world` container successfully run hole bujbe sob thik ache.

---

## Note: RAM Optimization

Tomar RAM 8GB — eta minimum requirement exactly pura kore, kintu Docker chalanor shomoy jodi multiple heavy container run koro tahole system slow lagte pare, cause WSL2 nijei kichu RAM eat kore.

Bhalo hoy `.wslconfig` file diye WSL2 er memory usage limit set kore rakhle:

```
[wsl2]
memory=4GB
```

File location: `%USERPROFILE%\.wslconfig`

Eta korle WSL2 max 4GB use korbe, baki RAM Windows er onno kaj er jonno free thakbe.

---

## Reference

Official docs: https://docs.docker.com/desktop/setup/install/windows-install/
