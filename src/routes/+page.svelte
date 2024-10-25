<script lang="ts">
	import RagPipeline from '$lib/RagPipeline.svelte'
import { Presentation, Slide, Code, Transition, Action } from '@animotion/core'
	import { tween } from '@animotion/motion'
	let text: HTMLParagraphElement
	let hidden = $state('hidden')
	let layout = $state('')
	let visibility = $state('')
	let stepNo = $state(0)

	let randomNum = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1) + min)
	let imageToDisplay = $state('many-sources')
</script>

<Presentation options={{ history: true, transition: 'slide', controls: true, progress: true, width: 1920, height: 1080, }}>
	<Slide class="h-full place-content-center place-items-center" out={() => (hidden = 'hidden')}>
		<Transition enter="blurry-enter" visible>
			<p class="text-8xl font-bold drop-shadow-sm">
				<img src="./logo.svg" alt="Climate RAG logo" class="w-96" />
			</p>
			<p class="mt-8 text-3xl" style="font-family: var(--r-climate-rag-font)">
				An AI-assisted research tool for energy and climate data
			</p></Transition
		>
		<Transition class={hidden} do={() => (hidden = 'hidden')} undo={() => (hidden = '')}>
			<div class="m-10 flex flex-row items-center gap-10 text-left">
				<div class="w-[300px]">
					<ul class="flex flex-col items-end text-right text-xl">
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								Ask open-ended research questions
							</li></Transition
						>
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								Let the model search for and scrape information buried deep in documents or websites
							</li>
						</Transition>
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								Multi-lingual and multi-strategy approach to finding key data
							</li>
						</Transition>
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								Supports scanned PDFs, dynamic websites, uploads
							</li>
						</Transition>
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								CLI tools to automate more complex research
							</li>
						</Transition>
						<Transition>
							<li
								style={`--r-max-width:${randomNum(20, 40)}ch; --r-arrow-v-offset:${randomNum(-1, -99)}%`}
								class="bubble text-zinc-900"
							>
								Support for several LLM models
							</li>
						</Transition>
					</ul>
				</div>
				<div class="h-[600px] grow">
					<video class="v-full h-full rounded-lg" src="./climate-rag.webm" muted autoplay loop>
					</video>
				</div>
			</div></Transition
		>
	</Slide>

	<Slide class="h-full place-content-center place-items-center">
		<Transition visible>
			<h1 class="text-7xl">What problem are we trying to solve?</h1>
		</Transition>

		<Transition
			enter="fade-enter"
			do={() => (layout = 'h-[600px]')}
			order={1}
			undo={() => {
				layout = ''
			}}
			class="hidden"
		>
			<div
				class="{layout} m-16 grid grid-cols-2 gap-10"
				style="grid-template-columns: minmax(0, 500px) 1fr;"
			>
				<div class="flex max-w-[400px] flex-col place-content-center gap-4 text-xl">
					<Transition enter="fade-enter" order={1} do={() => (imageToDisplay = 'many-sources')}>
						<div class="problem {imageToDisplay == 'many-sources' ? 'selected-problem' : ''}">
							Data often scattered across multiple sources and document formats.
						</div>
					</Transition>
					<Transition
						enter="fade-enter"
						order={2}
						do={() => (imageToDisplay = 'native-language')}
						undo={() => (imageToDisplay = 'many-sources')}
					>
						<div class="problem {imageToDisplay == 'native-language' ? 'selected-problem' : ''}">
							Sometimes, the best insights are disclosed in native language documents, rather than
							in English.
						</div>
					</Transition>
					<Transition enter="fade-enter" order={3} do={() => (imageToDisplay = 'long-report')}>
						<div class="problem {imageToDisplay == 'long-report' ? 'selected-problem' : ''}">
							Govt. and corporate reports are often long, unwieldy and unsearchable (due to scanned
							text).
						</div>
					</Transition>
					<Transition
						enter="fade-enter"
						order={4}
						do={() => (imageToDisplay = 'report-timeseries')}
					>
						<div class="problem {imageToDisplay == 'report-timeseries' ? 'selected-problem' : ''}">
							A time series dataset may be published across multiple reports, which is tedious to
							aggregate.
						</div>
					</Transition>
					<Transition
						enter="fade-enter"
						order={5}
						do={() => (imageToDisplay = 'brittle-scraping')}
						undo={() => (imageToDisplay = 'report-timeseries')}
					>
						<div class="problem {imageToDisplay == 'brittle-scraping' ? 'selected-problem' : ''}">
							Using a classical web scraper requires bespoke code for each source, and is brittle to
							changes in the source format.
						</div>
					</Transition>
				</div>

				<div class="flex place-content-center place-items-center">
					<div class="w-[500px]">
						<img
							class={imageToDisplay == 'many-sources' ? 'w-full' : 'hidden'}
							src="./many-sources.svg"
							height="300"
							alt="Many sources of data"
						/>
						<img
							class={imageToDisplay == 'native-language' ? 'w-full' : 'hidden'}
							src="./native-language.svg"
							height="300"
							alt="Graphic of a globe with different languages"
						/>
						<img
							class={imageToDisplay == 'long-report' ? 'w-fit' : 'hidden'}
							src="./long-report.gif"
							height="300"
							alt="Gif of a long report scrolling"
						/>
						<img
							class={imageToDisplay == 'report-timeseries' ? 'w-full' : 'hidden'}
							src="./report-timeseries.svg"
							height="300"
							alt="Time series data in reports"
						/>
						<img
							class={imageToDisplay == 'brittle-scraping' ? 'w-full' : 'hidden'}
							src="./brittle-scraping.svg"
							alt="Graphic of a brittle web scraper"
						/>
					</div>
				</div>
			</div>
		</Transition>
	</Slide>
	<Slide class="h-full place-content-center place-items-center" in={() => (layout = '')} out={() => {layout = ''
	}}>
		<Transition visible>
			<h1 class="text-7xl !text-yellow-300 static">The Solution</h1>
		</Transition>
		<Transition
			enter="enter"
			class="hidden"
			order={1}
			do={() => {
				layout = 'h-[600px]'
				visibility = ''
				stepNo = 1
			}}
			undo={() => {
				layout = ''
				visibility = ''
			}}
		>
			<div class="{layout} m-16 flex flex-col place-content-center place-items-center">
				<div
					class="{visibility} flex max-w-[50ch] flex-col place-content-center place-items-center text-xl"
				>
					<Transition enter="fade-enter" order={1} class="text-4xl">
						RAG <br /><span class="text-lg">aka</span><br />
						<strong>Retrieval Augmented Generation</strong>
					</Transition>
					<Transition enter="fade-enter" class="mt-16">
						This is a modern technique that combines the benefits of a database of verifiable
						information, with the flexibility of a large language generative model.
					</Transition>
				</div>
				<Transition
					enter="fade-enter"
					do={() => {
						visibility = 'hidden'
						stepNo = 0
					}}
					undo={() => {
						visibility = ''
						stepNo = 0
					}}
				>
				<RagPipeline stepNo={stepNo} />
				</Transition>
			</div>
		</Transition>
	</Slide>
	<Slide class="h-full place-content-center place-items-center" in={() => (layout = '')} out={() => {layout = ''
	}}>
		</Slide>
</Presentation>

<style>
	h1 {
		font-family: var(--r-heading-font);
		color: var(--r-heading-color);
		font-weight: 300;
	}

	.bubble {
		display: flex;
		align-items: center; /* Center content vertically */
		border-radius: 0px;
		max-width: var(--r-max-width);
		padding: 1px; /* Add some padding */
		padding-right: 10px; /* Add some padding to the right */
		padding-left: 10px; /* Add some padding to the left */
		position: relative; /* For positioning the tip */
		background-color: white; /* Ensure bubbles have a white background */
		margin-bottom: 10px; /* Add some margin to the bottom */
	}

	.bubble::before {
		content: '';
		position: absolute;
		top: 50%; /* Center vertically */
		left: 100%; /* Position at the right edge */
		transform: translateY(var(--r-arrow-v-offset)) translateX(-1px); /* Center the arrow vertically */
		border-top: 20px solid transparent;
		border-bottom: 10px solid transparent;
		border-left: 20px solid white; /* Arrow color */
	}

	.problem {
		display: grid;
		gap: 4em;
		padding: 10px;
		max-width: 40ch;
		color: var(--color-zinc-900, #18181b);
		background-color: white;
		box-shadow: 5px 5px 0px 0px rgba(255, 255, 255, 0.3);
		transition: box-shadow 0.3s;
	}

	.selected-problem {
		box-shadow: 10px 10px 0px 0px #bde352;
	}
</style>
