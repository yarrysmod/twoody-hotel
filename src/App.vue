<template>
	<div id="app" class="m-d-flex m-flex-column m-h-100">
		<!-- TODO: Tie into vue comps -->
		<AppSection
			:isShowing="$store.state.layout.isShowingBanner"
			@click="$store.commit('setIsShowingBanner', false)"
		>
			<div id="top-banner"/>
		</AppSection>

		<!-- Handle appSection click for navbar on chevron and ations instead.. -->
		<AppSection
			class="nav-section"
			is-showing
		>
			<NavBar/>
		</AppSection>

		<AppSection
			centered
			class="main-section m-flex-grow m-p-2"
			is-showing
		>
			<transition
				name="fade"
				mode="out-in"
			>
				<router-view id="content-wrapper"/>
			</transition>
		</AppSection>
		<AppSection
			:isShowing="$store.state.layout.isShowingFooter"
			@click="$store.commit('setIsShowingFooter', false)"
		>
			<div id="bottom-banner"/>
		</AppSection>
	</div>
</template>

<script>
import AppSection from "components/common/AppSection"
import NavBar from "components/nav/NavBar"

export default {
	name: "App",
	components:
		{
			AppSection,
			NavBar,
		},
	data: function()
	{
		return {
			isNavCollapsed: true,
		}
	},
	computed:
		{},
	created: function()
	{
	},
}
</script>

<style lang='less'>
@import "~styles/styles";
@import "~styles/modifiers";
@import (css) url('https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap');

html, body {
	height: 100%;
	margin: 0;
	padding: 0;
	width: 100%;

	background-color: @color-primary-triadic-1;
	color: @myblack;
}

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	//font-family: Avenir, Helvetica, Arial, sans-serif;
	font-family: 'Poppins', sans-serif;
}

#bottom-banner {
	background-color: @color-primary-triadic-3;
	bottom: 0;
	height: 50px;
}

#content-wrapper {
	background-color: @color-primary-triadic-1;
}

.main-section {
	flex: 1;
}

.nav-section {
	background-color: @color-primary-triadic-2;
}

#top-banner {
	background-color: @color-primary-triadic-3;
	height: 50px;
}

.fade-enter-active,
.fade-leave-active {
	transition-duration: 0.2s;
	transition-property: opacity;
	transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
	opacity: 0
}
</style>
