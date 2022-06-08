The general navbar for our project
<template>
	<div class="nav-wrapper">
		<div class="nav-items m-d-flex m-flex-content-center">
			<router-link
				class="nav-item"
				to="/"
			>
				Home
			</router-link>
			<router-link
				class="nav-item"
				to="/about"
			>
				About
			</router-link>
			<router-link
				class="nav-item"
				to="/maps"
			>
				Maps
			</router-link>
			<router-link
				class="nav-item"
				to="/amenities"
			>
				Amenities
			</router-link>
			<router-link
				v-if="!isLoggedIn && isDev"
				class="nav-item"
				to="/login"
			>
				Login
			</router-link>
		</div>
		<div
			v-if="isLoggedIn"
			class="user-items options-user"
		>
			<div class="user-item user-name">
				{{ userInitials }}
			</div>

			<div
				class="user-item user-action"
				@click="logout"
			>
				Logout
			</div>
		</div>
		<div
			v-else
			class="user-items options-guest"
		>
			<!-- Put any guest actions here -->
		</div>
	</div>
</template>

<script>
import firebase from "firebase"
import store from "@/store/store.js"

export default {
	name: "NavBar",
	computed:
		{
			/**
			 * @returns {string} - Users first name if loaded; Else empty string
			 */
			firstName ()
			{
				return store.state.user.user.firstName || ""
			},

			/**
			 * @returns {boolean} - Show certain only things while under development
			 */
			isDev ()
			{
				return parseFloat(process.env.VUE_APP_CI)
			},

			/**
			 * @returns {boolean} - Whether the app is initializing the user or not
			 */
			isLoadingData ()
			{
				return store.state.user.isLoggingIn
			},

			/**
			 * @returns {boolean} - Whether a user is logged in or not
			 */
			isLoggedIn ()
			{
				return store.state.user.isLoggedIn
			},

			/**
			 * @returns {string} - Users last name if loaded; Else empty string
			 */
			lastName ()
			{
				return store.state.user.user.lastName || ""
			},

			/**
			 * @returns {string} - Users initials to be displayed; Else dash
			 */
			userInitials ()
			{
				const first = this.firstName.length ? this.firstName[0].toUpperCase() : ""
				const last = this.lastName.length ? this.lastName[0].toUpperCase() : ""
				return (first + last) || "-"
			},
		},
	methods:
		{
			/**
			 * Logout the current user and remove the user session
			 *
			 * @returns {void}
			 */
			async logout ()
			{
				try
				{
					await firebase.auth().signOut()
				}
				catch (error)
				{
					console.error(
						error
					)
				}
				store.dispatch("logoutUser")
			},
		},
}
</script>

<style lang="less">
/* @todo setup a main file and set margins/padding there probably */
@import "~styles/styles.less";

@v-padding: 30px;

.nav-wrapper {
	.nav-items {
		.nav-item {
			padding: 1rem;
			display: inline-block;

			font-weight: bold;
			color: #2c3e50;
			transition: 0.2s ease-in-out;

			&.router-link-exact-active, &:hover {
				color: #42b983;
				background: @color-pastel-blue-focus;
			}
		}
	}

	.user-items {
		border: 1px solid black;
		border-radius: 50px;
		display: flex;
		flex-direction: column;
		flex-grow: 0;
		flex-shrink: 1;

		&.options-guest {
			border: none;
		}

		.user-item {
			margin: 3px 6px;
		}

		.user-action {
			border-top: 1px solid black;
			margin-bottom: 5px;
		}

		.user-name {
			margin-top: 5px;
		}
	}
}

</style>
