
<template>
    <div>
        <h2>Register</h2>
        <form @submit.prevent="register">
            <div>
                <label for="username">Username:</label>
                <input type="text" v-model="username" id="username" required>
            </div>
            <div>
                <label for="password">Password:</label>
                <input type="password" v-model="password" id="password" required>
            </div>
            <button type="submit">Register</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            username: "",
            password: ""
        };
    },
    methods: {
        async register() {
            try {
                const response = await fetch("/api/register", {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ username: this.username, password: this.password })
                });
                const data = await response.json();
                if (data.success) {
                    // Redirect to login page after successful registration
                    this.$router.push("/login");
                } else {
                    alert(data.error);
                }
            } catch (error) {
                alert("Registration failed: " + error.message);
            }
        }
    }
};
</script>
