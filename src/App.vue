<template>
    <nav id="nav" class="navbar is-primary" aria-label="main navigation">
        <div class="navbar-brand">
            <a
                role="button"
                class="navbar-burger"
                aria-label="menu"
                aria-expanded="false"
                data-target="navbarBasicExample"
            >
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
            </a>
        </div>

        <div id="navbarBasicExample" class="navbar-menu">
            <div class="navbar-start">
                <router-link class="navbar-item" to="/products"
                    >Products</router-link
                >
            </div>
        </div>
    </nav>
    <section>
        <div class="container">
            <router-view />
        </div>
    </section>
</template>

