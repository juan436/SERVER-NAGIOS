# Monitorización con Nagios

Este proyecto implementa un sistema de monitorización de red y servidores utilizando Nagios Core, integrado con Traefik como proxy inverso.

## Características

- Monitorización completa de red y servidores
- Interfaz web intuitiva
- Alertas configurables
- Integración con Docker
- Seguridad con HTTPS a través de Traefik
- Autenticación básica para el panel de control

## Requisitos Previos

- Docker y Docker Compose instalados
- Red Docker llamada `proxy` creada previamente
- Servidor Traefik configurado y en ejecución
- Dominio configurado para apuntar a tu servidor (por defecto: `nagios.tu-dominio.com`)

## Configuración

1. **Crea el directorio del proyecto**:
   ```bash
   mkdir -p ~/nagios
   cd ~/nagios
   ```

2. **Crea los directorios necesarios**:
   ```bash
   mkdir -p custom_nagios var/log/nagios var/archives var/rw
   ```

3. **Configura la contraseña de administrador**:
   - Genera una contraseña segura con:
     ```bash
     htpasswd -nb admin tu_contraseña_segura
     ```
   - Reemplaza la línea en `docker-compose.yml` con el resultado

## Despliegue

1. **Inicia el servicio de Nagios**:
   ```bash
   docker-compose up -d
   ```

2. **Verifica que el contenedor esté en ejecución**:
   ```bash
   docker ps
   ```

## Acceso

Una vez desplegado, podrás acceder a la interfaz de Nagios en:
- https://nagios.tu-dominio.com

**Credenciales por defecto**:
- Usuario: `admin`
- Contraseña: `nagiosadmin` (cámbiala en el paso de configuración)

## Personalización

### Cambiar el dominio
Para cambiar el dominio predeterminado, modifica la siguiente línea en `docker-compose.yml`:
```yaml
- "traefik.http.routers.nagios.rule=Host(`tu-dominio.com`)"
```

### Añadir hosts para monitorear
Puedes añadir configuraciones personalizadas en el directorio `custom_nagios/`.

## Seguridad

- Asegúrate de cambiar la contraseña por defecto
- El acceso está protegido por HTTPS y autenticación básica
- Mantén actualizada la imagen de Nagios

## Mantenimiento

### Actualizar Nagios
```bash
docker-compose pull
docker-compose up -d --force-recreate
```

### Ver logs
```bash
docker-compose logs -f
```

### Detener el servicio
```bash
docker-compose down
```

## Solución de Problemas

- **No se puede acceder al panel**: Verifica que el dominio esté configurado correctamente.
- **Problemas de autenticación**: Asegúrate de que la contraseña en el archivo `docker-compose.yml` esté correctamente configurada.
- **Ver logs de contenedor**: Usa `docker-compose logs -f` para ver los logs en tiempo real.

## Licencia

Este proyecto está bajo la licencia MIT.
