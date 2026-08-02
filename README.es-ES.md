

<h1 align="center">
Macbook Air 7,2 - Instrucciones de instalación manual de Arch Linux i3
</h1>
<p align="right">
 <a href="https://en.wikipedia.org/wiki/Copyleft">Copyleft</a>
 <br> Autor: <a href="mailto:adham.nasr@live.com">Adham Nasr</a>
 <br> <strong>
  Contrátame: <a href="https://propulsive.tech">Propulsive Technologies</a>
 </strong>
</p>

---

Este documento proporciona instrucciones sencillas pero detalladas sobre cómo instalar [Arch Linux][arch] en una [MacBook Air 7,2][MBA].

Tenga en cuenta que las instrucciones de instalación están diseñadas exclusivamente para funcionar en ese sistema en particular.

Por lo tanto, lea detenidamente este README antes de instalarlo en una máquina diferente.

[arch]: https://www.archlinux.org/
[MBA]: https://support.apple.com/kb/SP714?locale=en_US
---

## Tabla de contenidos

- [Especificaciones del dispositivo](#Device-Specs)
- [Qué funciona](#What-Works)
- [Preguntas frecuentes](#FAQ)
- Instalación:
  - [Parte 1](/Install-p1.md)
  - [Parte 2](/Install-p2.md)
  - [Parte 3](/Install-p3.md)
---

Hágase la vida más fácil
-------

 1. Lea el manual oficial ---> [DOCUMENTACIÓN DE INSTALACIÓN DE ARCH][docs]. Revise solo las primeras páginas sobre cómo instalar para tener una mejor comprensión de lo que está sucediendo.

 2. Lea todo el README antes de realizar cualquier acción.

 3. ¡Haga preguntas!

[docs]:https://wiki.archlinux.org/title/Installation_guide
---

Especificaciones del dispositivo y qué funciona
-------

### Especificaciones del dispositivo

       - Host: MacBookAir7,2 1.0
       - CPU: Intel i5-5250U (4) @ 2.700GHz
       - GPU: Intel HD Graphics 6000
       - Resolución máxima: 1440x900
       - Memoria: 4GiB
       - Almacenamiento: 120GiB
       - Bluetooth 4.0
       - Controlador de red: Adaptador de red inalámbrica BCM4360 802.11ac
       - Controlador multimedia: Cámara FaceTime HD 720p de Broadcom Inc.


### Qué funciona

  - [x] inicio inicial
  - [x] audio
  - [x] bluetooth
  - [x] wlan
  - [x] trackpad
  - [x] teclado
  - [x] webcam
  - [x] botones de función
  - [x] retroiluminación del teclado
  - [x] control de retroiluminación
  - [x] control de brillo
  - [ ] suspensión/hibernación+reactivación (solía funcionar, se realizará la solución de problemas)
---
---
Preguntas frecuentes (FAQ)
---

- ¿Cómo resolver los errores “no se puede bloquear la base de datos” o “no se pudo sincronizar ninguna base de datos”?
              
      # sudo rm /var/lib/pacman/db.lck
