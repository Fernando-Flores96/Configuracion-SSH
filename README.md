# Guía Completa: Configuración de Git y SSH

## 🎯 Configuración Inicial de Git

### Paso 1: Configurar tu identidad en Git
```bash
git config --global user.name "Carlos Flores"
git config --global user.email "kfflores96@gmail.com"
```

### Paso 2: Abrir el archivo de configuración global (opcional)
```bash
git config --global -e
```
**Para salir del editor:** Presiona `Esc` y luego escribe `:wq!` y presiona `Enter`

---

## 🔑 Configuración de Claves SSH

### Paso 1: Abrir Terminal
- **Windows:** Git Bash (incluido con Git para Windows)
- **Linux/macOS:** Terminal del sistema

### Paso 2: Verificar claves SSH existentes
```bash
ls -al ~/.ssh
```
Esto te mostrará si ya tienes claves SSH configuradas.

### Paso 3: Generar nueva clave SSH
```bash
ssh-keygen -t ed25519 -C "kfflores96@gmail.com"
```

**Durante la generación:**
1. **Ubicación:** Presiona `Enter` para aceptar la ruta por defecto
2. **Passphrase:** Opcional - puedes dejarla vacía o agregar una para mayor seguridad
3. **Confirmar passphrase:** Repite la passphrase si la configuraste

**Si tu sistema no soporta ed25519, usa:**
```bash
ssh-keygen -t rsa -b 4096 -C "kfflores96@gmail.com"
```

### Paso 4: Mostrar tu clave pública
```bash
cat ~/.ssh/id_ed25519.pub
```

**Tu clave pública generada es:**
```
ssh-ed25519 PPPPC3NzaJ1lZQE1NTE5MMMMILcz4AqdBIE1JHZRVIBgzec5ZSuiJigHy21cprhG+Qit kfflores96@gmail.com
```

---

## 🐙 Configuración en GitHub/GitLab

### Paso 1: Copiar la clave pública
Copia toda la línea que comienza con `ssh-ed25519` (la que obtuviste con el comando `cat`)

### Paso 2: Agregar la clave a GitHub
1. Ve a **GitHub.com** → **Settings** → **SSH and GPG keys**
2. Haz clic en **"New SSH key"**
3. **Title:** Ponle un nombre descriptivo (ej: "Laptop Personal")
4. **Key:** Pega tu clave pública completa
5. Haz clic en **"Add SSH key"**

### Paso 3: Agregar la clave a GitLab (si usas GitLab)
1. Ve a **GitLab.com** → **Preferences** → **SSH Keys**
2. Pega tu clave pública en el campo **Key**
3. **Title:** Nombre descriptivo
4. Haz clic en **"Add key"**

---

## ✅ Verificar la Conexión

### Probar conexión con GitHub
```bash
ssh -T git@github.com
```

**Respuesta esperada:**
```
Hi Carlos Flores! You've successfully authenticated, but GitHub does not provide shell access.
```

### Probar conexión con GitLab
```bash
ssh -T git@gitlab.com
```

---

## 🚀 Comandos Útiles Adicionales

### Iniciar el agente SSH (si es necesario)
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Ver configuración actual de Git
```bash
git config --list
```

### Cambiar la URL de un repositorio existente a SSH
```bash
# Ver la URL actual
git remote -v

# Cambiar de HTTPS a SSH
git remote set-url origin git@github.com:usuario/repositorio.git
```

---

## 🔧 Solución de Problemas Comunes

### Error: "Permission denied (publickey)"
1. Verifica que la clave esté agregada al agente SSH:
   ```bash
   ssh-add -l
   ```
2. Si no aparece, agrégala:
   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

### Error: "Could not open a connection to your authentication agent"
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Verificar que la clave pública sea correcta
```bash
cat ~/.ssh/id_ed25519.pub
```
Asegúrate de que coincida con la que agregaste a GitHub/GitLab.

---

## 📝 Notas Importantes

- **Nunca compartas tu clave privada** (`id_ed25519` sin `.pub`)
- **Solo comparte la clave pública** (`id_ed25519.pub`)
- **Usa HTTPS si SSH no funciona** en redes corporativas
- **La passphrase es opcional** pero recomendada para mayor seguridad

---

## ✨ Estado Actual

✅ **Configuración de Git completada**
✅ **Clave SSH generada correctamente**
✅ **Clave pública obtenida**

**Próximo paso:** Agregar la clave a GitHub/GitLab y probar la conexión.
