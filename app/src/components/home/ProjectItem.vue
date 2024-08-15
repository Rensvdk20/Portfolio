<template>
	<div class="project-item" :class="key % 2 == 0 ? 'reverse' : ''">
		<div class="project-item-image">
			<img :src="project.image" />
		</div>
		<div class="project-item-block">
			<p class="project-item-block-language">{{ project.languages }}</p>
			<a :href="project.link" target="_blank">
				<img src="/assets/images/icons/link.svg" class="project-item-block-link" />
			</a>
			<h3 class="project-item-block-name" :style="{ color: project.color }">
				{{ project.name }}
			</h3>
			<p class="project-item-block-description">{{ project.description }}</p>
		</div>
	</div>
</template>

<style lang="scss">
.project-item {
	padding: 80px 0;
	padding-left: 20px;
	padding-right: 20px;
	display: flex;
	justify-content: center;
	align-items: center;

	&-image img {
		max-width: 850px;
		border-radius: 25px;
		box-shadow: 6px 6px 4px 2px rgba(0, 0, 0, 0.25);
	}

	&-block {
		position: relative;
		max-width: 400px;
		margin-left: -150px;
		padding: 40px;
		background-color: $darkSecondary;
		border-radius: 25px;

		&-language {
			margin: 0 0 10px 0;
			max-width: 80%;
			font-size: 1.5rem;
			font-weight: 600;
		}

		&-link {
			position: absolute;
			top: 40px;
			right: 40px;
		}

		&-name {
			margin: 0;
			font-size: 2rem;
			font-weight: 700;
		}
	}

	&.reverse {
		background-color: $secondary;

		.project-item-image {
			order: 2;
		}

		.project-item-block {
			margin-left: 0;
			margin-right: -150px;
			order: 1;
		}
	}
}

@media #{$xxl} {
	.project-item {
		&-block {
			margin-left: -200px;
		}
	}
}

@media #{$lg} {
	.project-item {
		flex-direction: column;

		&-image {
			img {
				width: 100%;
			}
		}

		&-block {
			max-width: 75%;
			margin-top: -150px;
			margin-left: unset;
		}

		&.reverse {
			.project-item {
				&-block {
					order: 2;
					margin-right: 0;
				}

				&-image {
					order: 1;
				}
			}
		}
	}
}

@media #{$md} {
	.project-item {
		&-image img {
			box-shadow: 0px 0px 15px 5px rgba(0, 0, 0, 0.25);
		}

		&-block {
			max-width: 90%;
			margin-top: 25px;
			box-shadow: 0px 0px 15px 5px rgba(0, 0, 0, 0.25);
		}
	}
}

@media #{$sm} {
	.project-item {
		&-block {
			&-language {
				font-size: 1rem;
			}
		}
	}
}
</style>

<script setup lang="ts">
import { getCurrentInstance } from "vue";
import { type IProjectItem } from "@/interfaces/IProjectItem";

const props = defineProps<{
	project: IProjectItem;
}>();

const instance = getCurrentInstance();
const key = instance?.vnode.key as number;
</script>
