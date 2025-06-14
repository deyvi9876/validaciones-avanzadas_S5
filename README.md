Formulario con Validaciones Avanzadas
markdown
Copiar
Editar
# 🧠 Formulario Avanzado con Validaciones en JavaScript

Este proyecto consiste en un formulario moderno que implementa **validaciones personalizadas, seguridad de contraseñas, barra de progreso**, y restricciones como evitar copiar/pegar para mejorar la experiencia y protección del usuario.

---

## 🔧 Estructura de archivos

```bash

<input type="email" id="email" name="email"
       pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$" required>

<input type="password" id="password" name="password"
       pattern="^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[A-Za-z\d]{8,}$" required>
🔐 El patrón para la contraseña exige:

Mínimo 8 caracteres

Al menos 1 mayúscula

Al menos 1 minúscula

Al menos 1 número

🚫 Bloquear copiar/pegar en confirmación de contraseña
html
Copiar
Editar
<input type="password" id="confirmPassword" name="confirmPassword"
       onpaste="return false" oncopy="return false">
📶 Barra de fortaleza visual
html
Copiar
Editar
<div class="password-strength" id="strengthBar"></div>
🎨 CSS - Estilos de seguridad
css
Copiar
Editar
.password-strength {
    height: 6px;
    border-radius: 2px;
    margin-top: 5px;
    transition: all 0.3s ease;
}

.strength-weak { background-color: #e74c3c; width: 33%; }
.strength-medium { background-color: #f1c40f; width: 66%; }
.strength-strong { background-color: #2ecc71; width: 90%; }
.strength-very-strong { background-color: #3498db; width: 100%; }
📜 JavaScript - Lógica completa
🔍 Validación de fortaleza de contraseña
js
Copiar
Editar
function calcularFortalezaPassword(password) {
    let puntos = 0;
    if (password.length >= 8) puntos++;
    if (password.length >= 12) puntos++;
    if (/[a-z]/.test(password)) puntos++;
    if (/[A-Z]/.test(password)) puntos++;
    if (/[0-9]/.test(password)) puntos++;
    if (/[^A-Za-z0-9]/.test(password)) puntos++; // símbolos

    const niveles = ['muy débil', 'débil', 'media', 'fuerte', 'muy fuerte'];
    const nivel = Math.min(Math.floor(puntos / 1.2), 4);
    return { nivel, texto: niveles[nivel], puntos };
}
🎨 Mostrar barra según nivel
js
Copiar
Editar
function actualizarBarraFortaleza(fortaleza) {
    const barra = document.getElementById('strengthBar');
    const clases = [
        'strength-weak',
        'strength-weak',
        'strength-medium',
        'strength-strong',
        'strength-very-strong'
    ];
    if (barra) {
        barra.className = 'password-strength ' + clases[fortaleza.nivel];
    }
}
🚦 Evento al escribir contraseña
js
Copiar
Editar
document.addEventListener("DOMContentLoaded", function () {
    const passwordInput = document.getElementById('password');

    if (passwordInput) {
        passwordInput.addEventListener('input', function () {
            const password = this.value;
            const fortaleza = calcularFortalezaPassword(password);
            actualizarBarraFortaleza(fortaleza);
        });
    }
});
💡 Otras funcionalidades incluidas
Validaciones en tiempo real (oninput / onblur).

Mostrar resumen de datos ingresados al final.

Contador de caracteres dinámico en textarea.

Estilo de campos según validación (.valido, .error).

Bloqueo de envío si los campos no cumplen criterios.