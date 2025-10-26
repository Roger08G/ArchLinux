# 🐧 Sistema Arch Linux con Hyprland

Configuración completa de un entorno de escritorio Wayland moderno, minimalista y funcional con tema Nord.

## 📦 Componentes del Sistema

🧩 **Hyprland** → Compositor Wayland (gestor de ventanas)  
🎨 **Waybar** → Barra superior con información del sistema y lanzadores  
🧭 **Rofi** → Menú de aplicaciones con temas personalizados  
🐱 **Kitty** → Terminal moderna y rápida  
🖼️ **Waypaper/SWWW** → Gestor de fondos de pantalla  
🧰 **Kanshi** → Gestión de perfiles multi-monitor  
🔔 **Dunst** → Sistema de notificaciones  
🎵 **Playerctl** → Control de reproducción multimedia  
💡 **Starship** → Prompt elegante para la terminal  
📋 **Cliphist** → Historial de portapapeles  
🔒 **Swaylock** → Pantalla de bloqueo  
🧱 **Wlogout** → Menú de apagado/cierre de sesión

---

> Conectarse al Wifi

```bash
# Ver las redes WiFi disponibles
nmcli device wifi list

# Conectar a tu red WiFi
nmcli device wifi connect "NOMBRE_DE_TU_WIFI" password "tu_contraseña"
```

## 🚀 Instalación Completa Paso a Paso

### **PASO 1: Instalar Hyprland y dependencias básicas**

```bash
# Instalar Hyprland y herramientas esenciales
sudo pacman -S hyprland hyprpaper xdg-desktop-portal-hyprland \
               polkit-kde-agent qt5-wayland qt6-wayland

# Instalar AUR helper (yay) si no lo tienes
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd .. && rm -rf yay
```

### **PASO 2: Instalar todas las aplicaciones necesarias**

```bash
# Herramientas del sistema
sudo pacman -S waybar rofi-wayland kitty dunst kanshi \
               brightnessctl pavucontrol pamixer \
               network-manager-applet blueman \
               grim slurp wl-clipboard cliphist \
               thunar starship playerctl libnotify

# Desde AUR
yay -S swaylock-effects wlogout waypaper swww \
       ttf-cascadia-code-nerd nerd-fonts-complete
```

### **PASO 3: Instalar fuentes Nerd Font**

```bash
# Fuente principal (Cascadia Code)
yay -S ttf-cascadia-code-nerd

# Fuentes alternativas recomendadas
yay -S ttf-jetbrains-mono-nerd ttf-firacode-nerd
```

### **PASO 4: Clonar esta configuración**

```bash
# Respaldar configuraciones anteriores (si existen)
mkdir -p ~/.config-backup
mv ~/.config/hypr ~/.config-backup/ 2>/dev/null
mv ~/.config/waybar ~/.config-backup/ 2>/dev/null
mv ~/.config/rofi ~/.config-backup/ 2>/dev/null

# Clonar este repositorio
git clone https://github.com/Roger08G/ArchLinux.git ~/ArchLinux-config

# Copiar configuraciones al directorio correcto
cp -r ~/ArchLinux-config/hypr ~/.config/
cp -r ~/ArchLinux-config/waybar ~/.config/
cp -r ~/ArchLinux-config/rofi ~/.config/
cp -r ~/ArchLinux-config/kitty ~/.config/
cp -r ~/ArchLinux-config/dunst ~/.config/
cp -r ~/ArchLinux-config/kanshi ~/.config/
cp -r ~/ArchLinux-config/swaylock ~/.config/
cp -r ~/ArchLinux-config/wlogout ~/.config/
cp -r ~/ArchLinux-config/waypaper ~/.config/
```

### **PASO 5: Configurar carpeta de fondos de pantalla**

```bash
# Crear directorio para wallpapers
mkdir -p ~/Pictures/walls

# Descargar algunos fondos de ejemplo (opcional)
cd ~/Pictures/walls
wget https://images.unsplash.com/photo-1579547945413-497e1b99dac0 -O wallpaper1.jpg
wget https://images.unsplash.com/photo-1557683316-973673baf926 -O wallpaper2.jpg
```

### **PASO 6: Iniciar Hyprland**

```bash
# Si estás en TTY, simplemente ejecuta:
Hyprland

# O añadir a ~/.bash_profile o ~/.zprofile para inicio automático:
if [ -z "$DISPLAY" ] && [ "$XDG_VTNR" = 1 ]; then
  exec Hyprland
fi
```

---

## ⌨️ Atajos de Teclado Principales

### **Aplicaciones**
| Atajo | Acción |
|-------|--------|
| `SUPER + RETURN` | Abrir terminal (Kitty) |
| `SUPER + D` | Abrir menú de aplicaciones (Rofi) |
| `SUPER + C` | Abrir VS Code |
| `SUPER + S` | Abrir Spotify |
| `SUPER + W` | Abrir WhatsApp Web |
| `SUPER + O` | Abrir Obsidian |
| `SUPER + E` | Abrir gestor de archivos (Thunar) |
| `SUPER + B` | Abrir navegador (Brave) |
| `SUPER + G` | Cambiar fondo de pantalla (Waypaper) |
| `SUPER + P` | Captura de pantalla (selección) |

### **Gestión de Ventanas**
| Atajo | Acción |
|-------|--------|
| `SUPER + Q` | Cerrar ventana actual |
| `SUPER + F` | Pantalla completa |
| `SUPER + V` o `SUPER + SPACE` | Modo flotante |
| `SUPER + H/J/K/L` | Navegar entre ventanas (vim-style) |
| `SUPER + SHIFT + H/J/K/L` | Mover ventana actual |

### **Workspaces (Escritorios Virtuales)**
| Atajo | Acción |
|-------|--------|
| `SUPER + 1-9` | Ir al workspace 1-9 |
| `SUPER + SHIFT + 1-9` | Mover ventana al workspace 1-9 |

### **Sistema**
| Atajo | Acción |
|-------|--------|
| `SUPER + L` | Bloquear pantalla |
| `SUPER + X` | Menú de apagado (Wlogout) |
| `SUPER + SHIFT + R` | Recargar configuración de Hyprland |

---

## 🎨 Waybar - Barra Superior

### **Características:**
- 📊 Información en tiempo real: CPU, RAM, Batería, Red con IP
- 🎵 Lanzadores rápidos: VSCode, Spotify, WhatsApp
- 🕐 Reloj centrado con fecha
- 🔊 Control de volumen con scroll
- ☀️ Control de brillo con scroll
- 📡 Indicador de red WiFi/Ethernet con dirección IP

### **Recargar Waybar después de cambios:**
```bash
killall waybar && waybar &
```

### **Módulo de Red:**
Muestra el icono de red  junto con tu dirección IP actual:
- WiFi: ` 192.168.1.100`
- Ethernet: ` 192.168.1.50`

---

## 🖼️ Waypaper - Fondos de Pantalla

### **Uso:**
```bash
# Abrir selector visual de fondos
waypaper

# O usar el atajo
SUPER + G
```

### **Configuración automática:**
Los fondos se restauran automáticamente al iniciar Hyprland gracias a:
```bash
exec-once = waypaper --restore
```

---

## 🧭 Rofi - Menú de Aplicaciones

### **Uso:**
```bash
# Abrir menú de aplicaciones
SUPER + D
```

### **Temas personalizados:**
Los archivos de configuración están en `~/.config/rofi/`:
- `config.rasi` → Configuración principal
- `theme.rasi` → Tema visual personalizado

---

## 🐱 Kitty - Terminal

### **Atajos útiles:**
| Atajo | Acción |
|-------|--------|
| `CTRL + SHIFT + F5` | Recargar configuración sin cerrar |
| `CTRL + SHIFT + T` | Nueva pestaña |
| `CTRL + SHIFT + W` | Cerrar pestaña |

### **Cambiar tema:**
```bash
kitty +kitten themes
```

---

## 🔔 Dunst - Notificaciones

### **Características:**
- Notificaciones con blur y transparencia
- Integración con tema Nord
- Historial de notificaciones

### **Probar notificación:**
```bash
notify-send "Título de prueba" "Este es el mensaje de la notificación"
```

---

## 📺 Kanshi - Multi-Monitor

### **Configuración:**
Edita `~/.config/kanshi/config` para definir perfiles de monitores:

```bash
profile home {
    output eDP-1 enable mode 1920x1080@60Hz position 0,0
    output HDMI-A-1 enable mode 1920x1080@60Hz position 1920,0
}

profile laptop {
    output eDP-1 enable mode 1920x1080@60Hz position 0,0
}
```

Kanshi detectará automáticamente los monitores conectados y aplicará el perfil correspondiente.

---

## 🔒 Swaylock - Bloqueo de Pantalla

### **Uso:**
```bash
# Manual
SUPER + L

# Automático después de 10 minutos de inactividad (ya configurado)
```

### **Suspensión automática:**
El sistema se suspenderá después de 15 minutos de inactividad (configurado con `swayidle`).

---

## 🧱 Wlogout - Menú de Apagado

### **Uso:**
```bash
SUPER + X
```

### **Opciones disponibles:**
- 🔒 Bloquear
- 🚪 Cerrar sesión
- 💤 Suspender
- 🔄 Reiniciar
- ⚡ Apagar

---

## 📋 Cliphist - Historial de Portapapeles

### **Uso:**
El historial se guarda automáticamente. Para ver el historial:

```bash
# Ver historial de texto
cliphist list | rofi -dmenu | cliphist decode | wl-copy

# Ver historial de imágenes
cliphist list | grep -i 'image' | rofi -dmenu | cliphist decode | wl-copy
```

---

## 🔧 Solución de Problemas

### **Waybar no inicia:**
```bash
# Verifica errores
waybar -l debug

# Reinicia Waybar
killall waybar && waybar &
```

### **Rofi no muestra aplicaciones:**
```bash
# Actualiza cache de aplicaciones
rofi -show drun -modi drun
```

### **Las fuentes no se ven bien:**
```bash
# Actualiza cache de fuentes
fc-cache -fv
```

### **Hyprland no inicia:**
```bash
# Verifica logs
cat ~/.local/share/hyprland/hyprland.log
```

---

## 🎨 Personalización

### **Cambiar tema de colores:**
Los colores principales están en:
- `~/.config/waybar/style.css` → Waybar
- `~/.config/rofi/theme.rasi` → Rofi
- `~/.config/hypr/hyprland.conf` → Bordes y decoraciones

### **Tema actual:** Nord
- Background: `#2e3440`
- Foreground: `#eceff4`
- Accent: `#88c0d0` (azul Nord)

---

## 📚 Recursos Adicionales

- [Documentación oficial de Hyprland](https://wiki.hyprland.org)
- [Waybar Wiki](https://github.com/Alexays/Waybar/wiki)
- [Rofi Documentation](https://github.com/davatorium/rofi)
- [Nerd Fonts](https://www.nerdfonts.com)

---

## 📝 Notas Finales

- **Fuente requerida:** Cascadia Code Nerd Font o JetBrains Mono Nerd Font
- **Sistema:** Arch Linux con kernel 6.x o superior
- **GPU:** Compatible con drivers modernos (Mesa, NVIDIA 545+)
- **Tema:** Nord con transparencias y blur

**¡Disfruta de tu nuevo entorno Hyprland!** 🚀
