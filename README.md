# ConfiguraTuServidor
Iré dejando una serie de consejos o formas de configurar tu servidor y distintos servicios y utilidades.

## Servicios

* **Listar servicios**
`systemctl --type=service`
`systemctl list-unit-files`

* **Servicios en red**
` netstat -putona`

* **Crear servicio**
Ir a la carpeta `/etc/systemd/system` y crear un fichero con el nombre del servicio que quieras crear terminado en .service. Por ejemplo: `mi-servicio.service`.
	
* Y dentro del fichero escribimos algo como esto:	
	 ```
	[Unit]
	Description=My servicio X

	[Service]
	WorkingDirectory=/directorio-ejecucion
	ExecStart=/comando-a-ejecutar parametro/s que recibe
	Restart=always
	RestartSec=10 # Restart service after 10 seconds if dotnet service crashes

	[Install]
	WantedBy=multi-user.target
	```
	Posteriormente ejecutamos `systemctl daemon-reload` para que cargue el fichero y ya podremos usar los comandos con `systemctl` para iniciar, parar, reiniciar y detener nuestro servicio.
	 
## Seguridad
### UFW (Uncomplicated Firewall) <sup>Más en:  [linode](https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/)</sup>
**Activar/desactivar el firewall**
```sudo ufw enable```
```sudo ufw disable```

**Listar las aplicaciones o servicios disponible (Los que tienen nombre).**
```sudo ufw app list```
    
**Abrir o cerrar un puerto/servicio**
```sudo ufw default allow PUERTO/NombreServicio```
```sudo ufw default deny PUERTO/NombreServicio```

**IMPORTANTE: Despues de modificar las reglas**
Es necesario notificar al firewall lo cambios realizados mediante:  
```sudo ufw reload```
	

