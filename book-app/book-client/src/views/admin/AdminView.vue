<script setup>
import AdminMenu from '@/components/admin/AdminMenu.vue';
import { RouterLink } from 'vue-router';

</script>

<template>
	<div class="admin-container">
        <AdminMenu />
		<section class="admin-content">
			<h2>Admin Dashboard</h2>
			<div class="dashboard-container">
				<h3>What do you want to see?</h3>
				<RouterLink to="/admin-users">Users</RouterLink>
				<RouterLink to="/admin-books">Books</RouterLink>
			</div>
		</section>
	</div>
</template>

<style lang="scss" scoped>
.admin-container {
	display: flex;
    flex-direction: column;
    width: 100%;
	background-color: $color-primary;
    min-height: 100dvh;
	.admin-content {
		grid-column: 3 / span 10;
		min-height: 90dvh;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		gap: 3rem;
		margin: 5rem 1rem 1rem 1rem; 
		background-color: $color-background;
		border-radius: 16px;
		h2 {
			font-family: $font-title;
			font-size: $h-medium;
			margin-top: 3rem;
			margin-left: 2rem;
            margin-bottom: 1rem
		}
		.dashboard-container {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			flex-wrap: wrap;
			gap: 2rem;
			h3 {
				font-family: $font-paragraph;
				font-size: $h-small;
				flex-basis: 100%;
				text-align: center;
			}
			a {
				font-family: $font-paragraph;
				font-size: $h-small-mobile;
				text-decoration: none;
				color: $color-white;
				background-color: $color-secondary;
				padding: 1rem 2rem;
				border-radius: 8px;
				transition: 0.3s ease-in-out;
			}
			a:hover {
				background-color: $color-primary;
			}
		}
	}
}

@media screen and (min-width: 768px) {
    .admin-container {
        display: grid;
        grid-template-columns: repeat(12, 1fr);
        .admin-content {
            // width: auto;
            grid-column: 3 / span 10;
            margin: 1rem;
			.dashboard-container {
				flex-direction: row;
				justify-content: flex-start;
				margin-left: 2rem;
			}
        }
    }
}
</style>
