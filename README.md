# Dotfiles Backup and Restore

This repository contains my Hyprland dotfiles for Arch Linux, stored in a bare Git repository.

## **Restoring Dotfiles & Installed Packages on a New System**

### **1️⃣ Restore Dotfiles**
Clone your dotfiles repository:
```bash
git clone --bare https://github.com/yourusername/dotfiles.git $HOME/.dotfiles
alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'
dotfiles checkout
```

If you get errors about existing files, move them:
```bash
mkdir -p ~/.dotfiles-backup-existing
rsync --recursive --verbose --backup --suffix=.bak $HOME/.config ~/.dotfiles-backup-existing/
dotfiles checkout
```

---

### **2️⃣ Restore Installed Packages**

#### **Restore `pacman` Packages**
```bash
sudo pacman -S --needed - < ~/.dotfiles-backup/pacman-packages.txt
```

#### **Restore `yay` Packages**
First, install `yay` if not installed:
```bash
sudo pacman -S --needed yay
```
Then restore all AUR packages:
```bash
yay -S --needed - < ~/.dotfiles-backup/yay-packages.txt
```

Now, your system is restored with all your configurations and packages! 🚀



## 🚀 Restoring Dotfiles on a New System

Follow these steps to restore your dotfiles on a fresh system.

### **1️⃣ Install Required Packages**
Before cloning the dotfiles, install the necessary packages:
```bash
sudo pacman -S --needed git
```

### **2️⃣ Clone the Dotfiles Repository**
Since the dotfiles are stored in a **bare Git repository**, use the following command to clone it:
```bash
git clone --bare https://github.com/JUSTMEETPATEL/dotfiles.git $HOME/.dotfiles
```

### **3️⃣ Set Up the `dotfiles` Alias**
To easily manage the dotfiles, define an alias:
```bash
alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'
```
Make this alias permanent by adding it to your shell config:
```bash
echo "alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'" >> ~/.bashrc
source ~/.bashrc  # Reload shell configuration
```

### **4️⃣ Checkout the Dotfiles**
Run the following command to apply the dotfiles:
```bash
dotfiles checkout
```
If you encounter errors due to existing files, run:
```bash
dotfiles checkout -f
```

### **5️⃣ Prevent Untracked Files from Showing**
To avoid unnecessary warnings from Git:
```bash
dotfiles config --local status.showUntrackedFiles no
```

### **6️⃣ Install Hyprland and Dependencies**
Since these dotfiles are for Hyprland, install it along with necessary dependencies:
```bash
sudo pacman -S hyprland waybar kitty rofi
```
> You may need additional packages depending on your setup (e.g., `sddm`, `nvidia` drivers, etc.).

### **7️⃣ Reboot and Enjoy!**
After setting up everything, restart your system:
```bash
reboot
```
Once logged in, Hyprland should load with your dotfiles applied! 🎉

---

## 📌 Notes
- If you modify your dotfiles, use the following to update and push changes:
  ```bash
  dotfiles add ~/.config/hypr
  dotfiles commit -m "Updated Hyprland config"
  dotfiles push
  ```
- If you need to ignore certain files from being tracked, add them to:
  ```bash
  ~/.dotfiles/info/exclude
  ```

---

### ✅ Your Hyprland setup is now backed up and easily restorable on any Arch-based system!

