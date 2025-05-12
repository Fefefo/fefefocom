<script lang="ts">
	import emblaCarouselSvelte from 'embla-carousel-svelte';
	import type { EmblaCarouselType, EmblaOptionsType } from 'embla-carousel';
	import SdepdleIcon from '$lib/icons/sdepdle.png';
	import MemoryIcon from '$lib/icons/memory.png';
	import TacoIcon from '$lib/icons/taco.png';
	let emblaApi: EmblaCarouselType;

	let selectedIndex = $state(0);

	const slides = [
		{
			name: 'TACO',
			url: 'https://taco.fefefo.com',
			pic: TacoIcon
		},
		{
			name: 'MEMORY',
			url: 'https://memory.fefefo.com',
			pic: MemoryIcon
		},
		{
			name: 'SDEPDLE',
			url: 'https://sdepdle.fefefo.com',
			pic: SdepdleIcon
		},
		{
			name: 'TACO',
			url: 'https://taco.fefefo.com',
			pic: TacoIcon
		},
		{
			name: 'MEMORY',
			url: 'https://memory.fefefo.com',
			pic: MemoryIcon
		},
		{
			name: 'SDEPDLE',
			url: 'https://sdepdle.fefefo.com',
			pic: SdepdleIcon
		}
	];

	// function logSlidesInView(emblaApi: EmblaCarouselType): void {
	// 	console.log(emblaApi.slidesInView());
	// }

	function selectSlide(emblaApi: EmblaCarouselType) {
		selectedIndex = emblaApi.selectedScrollSnap();
	}

	function onInit(event: CustomEvent<EmblaCarouselType>) {
		emblaApi = event.detail;
		// emblaApi.scrollNext();
		// emblaApi.on('slidesInView', logSlidesInView);
		emblaApi.on('select', selectSlide);
		// console.log(emblaApi.slidesInView);
	}
	let options: EmblaOptionsType = { loop: true };

	let clientWidth = $state(0);
</script>

<svelte:window bind:innerWidth={clientWidth} />

<div class="grid min-h-screen grid-rows-[auto_1fr_auto]">
	<!-- Header -->
	<header class="p-10"></header>
	<!-- Page -->
	<div class="container mx-auto grid grid-cols-1 xl:grid-cols-[200px_minmax(0px,_1fr)_200px]">
		<!-- Sidebar (Left) -->
		<!-- NOTE: hidden in smaller screen sizes -->
		<aside class="sticky top-0 col-span-1 hidden p-4 xl:block"></aside>
		<!-- Main -->
		<main class="col-span-1 h-full space-y-4 p-4">
			<h1 class="pb-16 text-center font-[Medodica] text-7xl">fefefo.com</h1>

			<div class="grid grid-cols-12 items-center">
				<div class="col-span-1 flex items-center justify-center">
					<!-- svelte-ignore a11y_consider_explicit_label -->
					<button
						class="btn flex h-6 w-6 cursor-pointer items-center justify-center rounded-full border-2 border-orange-500 bg-orange-200 p-3 md:h-10 md:w-10 lg:h-14 lg:w-14"
						onclick={() => {
							emblaApi.scrollPrev();
						}}
					>
						<iconify-icon
							class="stroke-black stroke-[1.5]"
							icon="pixelarticons:chevron-left"
							width={clientWidth > 1024 ? 30 : clientWidth > 768 ? 20 : 10}
							heigth={clientWidth > 1024 ? 30 : clientWidth > 768 ? 20 : 10}
						></iconify-icon>
					</button>
				</div>
				<div
					class="embla col-span-10 overflow-hidden select-none"
					use:emblaCarouselSvelte={{ options, plugins: [] }}
					onemblaInit={onInit}
				>
					<div class="embla__container flex">
						{#each slides as slide, index}
							<div class="embla__slide z-10 flex min-w-1/3 items-center justify-center">
								<div
									class="flex w-full max-w-full items-center justify-center rounded-lg bg-blue-500 text-center text-white shadow-lg duration-200 {index ==
									selectedIndex
										? ''
										: 'scale-75'}"
								>
									{#if index == selectedIndex}
										<a
											href={slide.url}
											class="flex max-w-full flex-col items-center justify-center gap-3 px-1 py-1 md:px-0 md:py-3"
										>
											<img src={slide.pic} alt="" class="max-h-14 sm:max-h-32" />
											<p class="hidden font-[Superfats] font-semibold tracking-widest md:block">
												{slide.name}
											</p>
										</a>
									{:else}
										<div
											class="flex max-w-full flex-col items-center justify-center gap-3 px-1 py-1 md:px-0 md:py-3"
										>
											<img src={slide.pic} alt="" class="max-h-10 sm:max-h-32" />
											<p class="hidden font-[Superfats] font-semibold tracking-widest md:block">
												{slide.name}
											</p>
										</div>
									{/if}
								</div>
							</div>
						{/each}
					</div>
				</div>
				<div class="col-span-1 flex items-center justify-center">
					<!-- svelte-ignore a11y_consider_explicit_label -->
					<button
						class="btn flex h-6 w-6 cursor-pointer items-center justify-center rounded-full border-2 border-orange-500 bg-orange-200 p-3 md:h-10 md:w-10 lg:h-14 lg:w-14"
						onclick={() => {
							emblaApi.scrollNext();
						}}
					>
						<iconify-icon
							class="stroke-black stroke-[1.5]"
							icon="pixelarticons:chevron-right"
							width={clientWidth > 1024 ? 30 : clientWidth > 768 ? 20 : 10}
							heigth={clientWidth > 1024 ? 30 : clientWidth > 768 ? 20 : 10}
						></iconify-icon>
						<!-- <svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							{...$$props}
						>
							<path
								fill="currentColor"
								d="M8 5v2h2V5zm4 4V7h-2v2zm2 2V9h-2v2zm0 2h2v-2h-2zm-2 2v-2h2v2zm0 0h-2v2h2zm-4 4v-2h2v2z"
								stroke-width="1.5"
								stroke="currentColor"
							/>
						</svg> -->
					</button>
				</div>
			</div>
		</main>
		<!-- Sidebar (Right) -->
		<!-- NOTE: hidden in smaller screen sizes -->
		<aside class="sticky top-0 col-span-1 hidden p-4 xl:block"></aside>
	</div>
	<!-- Footer -->
	<footer class=" p-4"></footer>
</div>
