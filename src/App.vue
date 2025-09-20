<template>
    <div class="app-shell">
        <header class="main-nav">
            <div class="nav-brand">Programación Front End</div>
            <nav class="nav-links">
                <router-link to="/" exact>Cálculo de calificaciones</router-link>
                <router-link to="/Ejercicio2">Formulario de Registro</router-link>
            </nav>
        </header>
        <main class="content-area">
            <router-view />
        </main>
    </div>
</template>

<style scoped>
    .app-shell {
        min-height: 100vh;
        background-color: #f9fbfd;
        color: #2d3748;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .main-nav {
        display: flex;
        align-items: center;
        padding: 18px 48px;
        background-color: #ffffff;
        border-bottom: 1px solid #e2e8f0;
        box-shadow: 0 1px 4px rgba(15, 23, 42, 0.05);
        gap: 36px;
    }

    .nav-brand {
        font-size: 20px;
        font-weight: 600;
        color: #2d3748;
        white-space: nowrap;
    }

    .nav-links {
        display: flex;
        align-items: center;
        gap: 28px;
        font-size: 16px;
    }

    .nav-links a {
        color: #718096;
        text-decoration: none;
        transition: color 0.2s ease;
    }

    .nav-links a:hover {
        color: #2d3748;
    }

    .nav-links a.router-link-exact-active,
    .nav-links a.router-link-active {
        color: #2d3748;
        font-weight: 500;
    }

    .content-area {
        padding: 32px 24px 48px;
    }
</style>
