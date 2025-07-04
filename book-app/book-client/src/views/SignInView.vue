<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import AuthView from '../components/AuthView.vue';
import useAuthStore from '@/stores/useAuthStore';
import LoadingBar from '@/components/LoadingBar.vue';

const username = ref('');
const password = ref('');
const router = useRouter();
const error = ref('');
const loading = ref(false);

const useAuth = useAuthStore();

async function handleLogin() {
	loading.value = true;
	await useAuth.login(username.value, password.value);
	loading.value = false;
	if (useAuth.error !== null) {
		error.value = useAuth.error;
	}
	router.push('/admin');
}

if (useAuth.isAuthenticated) {
	router.push('/admin');
}
</script>

<template>
	<AuthView
		:title="'Welcome to The Lumos Library'"
		:submitText="'Log in'"
		:onSubmitHandler="handleLogin"
		:errorMessage="error"
		@update:username="username = $event"
		@update:password="password = $event"
	>
		<template #goBackLink>
			<RouterLink to="/" class="authview-go-back-link">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					height="24px"
					viewBox="0 -960 960 960"
					width="24px"
					fill="#1f1f1f"
				>
					<path d="m313-440 224 224-57 56-320-320 320-320 57 56-224 224h487v80H313Z" />
				</svg>
				<span>Back</span>
			</RouterLink>
		</template>

		<button class="authview-form-button" type="button" @click="router.push('/register')">Register</button>

		<template #loginWithoutSignInLink>
			<div class="authview-sign-in-without-login-wrapper">
				<RouterLink to="/" class="authview-form-button">Continue without signing in</RouterLink>
			</div>
		</template>
	</AuthView>
	<div v-if="loading" class="loading-container">
		<LoadingBar />
	</div>
</template>

<style lang="scss" scoped>
.loading-container {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	z-index: 10;
	width: 100dvw;
	height: 100dvh;
	// background-color: $color-background;
	// filter: blur(2px);
	backdrop-filter: blur(2px);
	-webkit-backdrop-filter: blur(2px);
	display: flex;
	justify-content: center;
	align-items: center;
	div {
		color: white;
	}
}

.authview-form-button {
	border-radius: $border-small;
	background-color: $color-red;
	box-shadow: $drop-shadow;
	color: $color-white;
	min-height: 48px;
	min-width: 48px;
	padding: 0.75rem 1.25rem;
	margin-bottom: 1rem;
	margin-top: 1rem;
	text-decoration: none;
	font-family: $font-title;
	padding-right: 2rem;
	padding-left: 2rem;
	font-size: $h-small-mobile;
	transition: 0.2s ease-in-out;
	cursor: pointer;
}

.authview-form-button:hover {
	background-color: $color-secondary;
}

.authview-sign-in-without-login-wrapper {
	text-align: center;
	width: 100%&;
	margin-bottom: 1rem;
	font-size: $h-small-mobile;
	margin-top: 1rem;
}

.authview-go-back-link {
	text-align: left;
	display: flex;
	align-items: center;
	margin-top: 1rem;
	margin-left: 1rem;
	text-decoration: none;
	color: $color-black;
	margin-bottom: 2rem;
    transition: 0.2s ease-in-out;
}

.authview-go-back-link:hover {
    cursor: pointer;
    color: $color-red;
}

@media (min-width: 700px) {
	.authview-go-back-link {
		margin-top: 0;
		margin-bottom: 4rem;
	}
}

@media (min-width: 1200px) {
	.authview-form-button {
		font-size: $h-small-mobile;
		padding-right: 5rem;
		padding-left: 5rem;
	}
}
</style>
