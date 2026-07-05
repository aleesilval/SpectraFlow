# SpectraFlow 🌊

## Estado del repositorio

- `firmware` ahora está incluido como submódulo (preserva su historial).
- Repositorio configurado como **privado** según la visibilidad actual.
- Git LFS está habilitado para los binarios y archivos grandes relevantes.
- La carpeta local `firmware-repo/` (copia temporal del historial) ha sido eliminada.

Para obtener el submódulo al clonar el repositorio por primera vez:

```bash
git clone --recurse-submodules https://github.com/aleesilval/SpectraFlow.git
```

Si ya clonaste el repo sin submódulos:

```bash
git submodule update --init --recursive
```

Contacto: propietario del repo `aleesilval`.
