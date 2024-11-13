<script lang="ts">
	import Roadmap from '$lib/Roadmap.svelte'
	import RagPipeline from '$lib/RagPipeline.svelte'
	import PPAExample from '$lib/PPAExample.svelte'
	import { Presentation, Slide, Code, Transition, Action } from '@animotion/core'
	let hidden = $state('hidden')
	let layout = $state('')
	let visibility = $state('')
	let stepNo = $state(0)
	let grid_n_cols = $state('grid-cols-1')
	let headingClasses = $state('')

	let randomNum = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1) + min)
	let imageToDisplay = $state('many-sources')
	import ComparisonCard from '$lib/ComparisonCard.svelte'


</script>

<Presentation
	options={{
		history: import.meta.env.VITE_DEV || false,
		transition: 'slide',
		controls: true,
		progress: true,
		width: 1920,
		height: 1080
		// disableLayout = false autoscales the slides to fit the screen
		// disableLayout: false
	}}
>
	<Slide class="h-full place-content-center place-items-center" out={() => (hidden = 'hidden')}>
		<Transition enter="blurry-enter" visible>
			<p class="text-8xl font-bold drop-shadow-sm">
				<img src="./logo.svg" alt="Climate RAG logo" class=" w-56 xl:w-96" />
			</p>
			<p class="mt-4 text-xl xl:mt-8 xl:text-3xl" style="font-family: var(--r-climate-rag-font)">
				An AI-assisted research tool for energy and climate data
			</p>
			<p class="block text-sm sm:hidden">
				This presentation isn't yet suitable for mobile screens.
			</p>
		</Transition>
		<Transition class={hidden} do={() => (hidden = 'hidden')} undo={() => (hidden = '')}>
			<div class="m-5 flex flex-row items-center gap-5 text-left xl:m-10 xl:gap-10">
				<div class="w-[30vw] max-w-[300px]">
					<ul class="flex flex-col items-end text-right text-sm xl:text-xl">
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
				<div class="h-[65vh] grow">
					<video
						class="v-full h-full rounded-sm shadow-[5px_5px_10px_#89b2647a]"
						src="./climate-rag.webm"
						muted
						autoplay
						loop
					>
					</video>
				</div>
			</div></Transition
		>
	</Slide>

	<Slide class="h-full place-content-center place-items-center">
		<Transition visible>
			<h1 class="text-4xl xl:text-4xl xl:text-7xl">What problems are we trying to solve?</h1>
		</Transition>

		<Transition
			enter="fade-enter"
			do={() => (layout = 'h-[70vh]')}
			order={1}
			undo={() => {
				layout = ''
			}}
			class="hidden"
		>
			<div
				class="{layout} 300px)_1fr] m-8 grid grid-cols-2 grid-cols-[minmax(0, gap-5 xl:m-16 xl:grid-cols-[minmax(0,_500px)_1fr] xl:gap-10"
			>
				<div
					class="flex max-w-[600px] flex-col place-content-center gap-4 text-sm xl:max-w-[400px] xl:text-xl"
				>
					<Transition enter="fade-enter" order={1} do={() => (imageToDisplay = 'many-sources')}>
						<div class="problem {imageToDisplay == 'many-sources' ? 'highlighted-block' : ''}">
							Data often scattered across multiple sources and document formats.
						</div>
					</Transition>
					<Transition
						enter="fade-enter"
						order={2}
						do={() => (imageToDisplay = 'native-language')}
						undo={() => (imageToDisplay = 'many-sources')}
					>
						<div class="problem {imageToDisplay == 'native-language' ? 'highlighted-block' : ''}">
							Sometimes, the best insights are disclosed in native language documents, rather than
							in English.
						</div>
					</Transition>
					<Transition enter="fade-enter" order={3} do={() => (imageToDisplay = 'long-report')}>
						<div class="problem {imageToDisplay == 'long-report' ? 'highlighted-block' : ''}">
							Govt. and corporate reports are often long, unwieldy and unsearchable (due to scanned
							text).
						</div>
					</Transition>
					<Transition
						enter="fade-enter"
						order={4}
						do={() => (imageToDisplay = 'report-timeseries')}
					>
						<div class="problem {imageToDisplay == 'report-timeseries' ? 'highlighted-block' : ''}">
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
						<div class="problem {imageToDisplay == 'brittle-scraping' ? 'highlighted-block' : ''}">
							Using a classical web scraper requires bespoke code for each source, and is brittle to
							changes in the source format.
						</div>
					</Transition>
				</div>

				<div class="flex place-content-center place-items-center">
					<div class="w-[30vw]">
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
	<Slide
		class="h-full place-content-center place-items-center"
		in={() => (layout = '')}
		out={() => {
			layout = ''
		}}
	>
		<h1 class="text-4xl xl:text-7xl">Case studies</h1>
	</Slide>
	<Slide class="h-full place-content-center place-items-center">
		<Transition visible enter="fade-enter">
			<div class="mt-5 block max-w-[80ch] text-left text-xs xl:text-lg">
				<div class="border-l border-l-[var(--r-heading-color)] pl-5 font-mono">
					What is the FiT tariff won by the Taqa Arabia solar plant in Egypt?
				</div>
				<p class="pt-2">
					Answering this question is contingent on the model finding the right document and not
					getting confused by conflicting evidence.
				</p>
			</div>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			do={() => {
				layout = 'h-[70vh]'
			}}
			undo={() => {
				layout = ''
			}}
			order={1}
		>
			<div class="{layout} m-4 grid grid-cols-3 items-stretch gap-3 xl:m-16">
				<Transition enter="fade-enter" order={1}>
					<ComparisonCard
						title="ChatGPT"
						emoji="😐"
						imageUrl="./comparison_screenshots/chatgpt_taqa.png"
						imageAlt="Screenshot showing that ChatGPT knows the answer but doesn't provide any citations"
						lightboxDescription="ChatGPT knows the answer but doesn't provide any citations"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Perplexity AI"
						emoji="🎉"
						imageUrl="./comparison_screenshots/perplexity_taqa.png"
						imageAlt="Screenshot showing that Perplexity AI knows the answer"
						lightboxDescription="Perplexity AI knows the answer, and also returns superfluous information"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Climate RAG"
						emoji="🎉"
						imageUrl="./comparison_screenshots/climate-rag_taqa.png"
						imageAlt="Screenshot showing that Climate RAG knows the answer"
						lightboxDescription="Climate RAG knows the answer and only returns relevant information"
					/>
				</Transition>
			</div></Transition
		>
	</Slide>
	<Slide class="h-full place-content-center place-items-center">
		<Transition visible enter="fade-enter">
			<div class="mt-5 block max-w-[80ch] text-left text-xs xl:text-lg">
				<div class="border-l border-l-[var(--r-heading-color)] pl-5 font-mono">
					What is the total electricity generated by Camden power station in each month of 2023?
					Return the result as a table with columns Power station name, Date (Month-Year),
					Generation (GWh).
				</div>
				<p class="pt-2">
					Answering this question is contingent on the model identifying multiple scanned documents
					and referencing small chunks of text from each
				</p>
			</div>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			do={() => {
				layout = 'h-[70vh]'
			}}
			undo={() => {
				layout = ''
			}}
			order={1}
		>
			<div class="{layout} m-4 grid grid-cols-3 items-stretch gap-3 xl:m-16">
				<Transition enter="fade-enter" order={1}>
					<ComparisonCard
						title="ChatGPT"
						emoji="👎"
						lightboxDescription="ChatGPT doesn't know the answer"
						imageUrl="./comparison_screenshots/chatgpt_camden.png"
						imageAlt="Screenshot showing that ChatGPT doesn't know the answer"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Perplexity AI"
						emoji="👎"
						lightboxDescription="Perplexity AI doesn't know the answer"
						imageUrl="./comparison_screenshots/perplexity_camden.png"
						imageAlt="Screenshot showing that Perplexity AI doesn't know the answer"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Climate RAG"
						emoji="🎉"
						lightboxDescription="Climate RAG knows the answer and only returns relevant information"
						imageUrl="./comparison_screenshots/climate-rag_camden.png"
						imageAlt="Screenshot showing that Climate RAG knows the answer"
					/>
				</Transition>
			</div></Transition
		>
	</Slide>
	<Slide class="h-full place-content-center place-items-center">
		<Transition visible enter="fade-enter">
			<div class="mt-5 block max-w-[80ch] text-left text-xs xl:text-lg">
				<div class="border-l border-l-[var(--r-heading-color)] pl-5 font-mono">
					For the countries in the list, give me a table outlining which countries have PPAs or
					liberalised power markets, and fuel-price pass through for gas power plants: Bahrain,
					Bangladesh, Chile, Cote d'Ivoire, Egypt, Ghana, Indonesia, Iraq, Kuwait, Mozambique,
					Myanmar, Nigeria, Philippines, [...]
				</div>
				<p class="pt-2">
					Answering this question is contingent on the model running multiple queries, one for each
					country on the list, and then collating the results together.
				</p>
			</div>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			do={() => {
				layout = 'h-[70vh]'
			}}
			undo={() => {
				layout = ''
			}}
			order={1}
		>
			<div class="{layout} m-4 grid grid-cols-3 items-stretch gap-3 xl:m-16">
				<Transition enter="fade-enter" order={1}>
					<ComparisonCard
						title="ChatGPT"
						emoji="😐"
						lightboxDescription="ChatGPT creates a plausible looking tables, but without any country-specific citations"
						imageUrl="./comparison_screenshots/chatgpt_ppa.png"
						imageAlt="Screenshot showing that ChatGPT creates a plausible looking table, but without any country-specific citations"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Perplexity AI"
						emoji="👎"
						lightboxDescription="Perplexity AI doesn't know the answer"
						imageUrl="./comparison_screenshots/perplexity_ppa.png"
						imageAlt="Screenshot showing that Perplexity AI doesn't know the answer"
					/>
				</Transition>

				<Transition enter="fade-enter">
					<ComparisonCard
						title="Climate-RAG"
						emoji="🎉"
						lightboxDescription="Climate RAG creates the correct table, with citations for each country. The queries were triggered manually using Climate RAG tools and formatted into a table using Google Gemini."
						imageUrl="./comparison_screenshots/climate-rag_ppa.png"
						imageAlt="Screenshot showing that Climate RAG knows the answer"
					/>
				</Transition>
			</div></Transition
		>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-center"
		in={() => (layout = '')}
		out={() => {
			layout = ''
		}}
	>
		<Transition visible>
			<h1 class="static text-4xl !text-yellow-300 xl:text-7xl">How Climate RAG works</h1>
		</Transition>
		<Transition
			enter="enter"
			class="hidden"
			order={1}
			do={() => {
				layout = 'h-[70vh]'
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
					class="{visibility} flex max-w-[50ch] flex-col place-content-center place-items-center text-sm xl:text-xl"
				>
					<Transition enter="fade-enter" order={1} class="text-2xl xl:text-4xl">
						RAG <br /><span class="text-sm xl:text-lg">aka</span><br />
						<strong>Retrieval Augmented Generation</strong>
					</Transition>
					<Transition enter="fade-enter" class="mt-16">
						This is a modern technique that combines the benefits of a database of verifiable
						information, with the flexibility of a large language generative model.
					</Transition>
				</div>
				<Transition
					enter="fade-enter"
					class=" h-[80vh] w-[80vw] xl:h-[85vh] xl:w-[85vw]"
					do={() => {
						visibility = 'hidden'
						stepNo = 0
						layout = 'h-[70vh]'
					}}
					undo={() => {
						visibility = ''
						stepNo = 0
						layout = 'h-[70vh]'
					}}
				>
					<RagPipeline {stepNo} />
				</Transition>
			</div>
		</Transition>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-center"
		out={() => {
			layout = 'h-[70vh]'
			visibility = 'hidden'
		}}>

			<h1 class="{headingClasses} static text-4xl !text-yellow-300 xl:text-7xl">
				Running complex research queries
			</h1>
			</Slide>
	<Slide
		class="h-full place-content-center place-items-center"
		in={() => {
			headingClasses = ''
			layout = ''
		}}
	>
	<Transition
			visible
			enter="fade-enter"
			do={() => {
				headingClasses = ''
				hidden = 'opacity-0 hidden'
			}}
		>
			<div class="mt-5 block max-w-[80ch] text-left text-xs xl:text-lg">
				<div class="border-l border-l-[var(--r-heading-color)] pl-5 font-mono">
					For the countries in the list, give me a table outlining which countries have PPAs or
					liberalised power markets, and fuel-price pass through for gas power plants: Bahrain,
					Bangladesh, Chile, Cote d'Ivoire, Egypt, Ghana, Indonesia, Iraq, Kuwait, Mozambique,
					Myanmar, Nigeria, Philippines, [...]
				</div>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			order={1}
			do={() => {
				layout = 'h-[70vh]'
				stepNo = 1
				headingClasses = 'text-left pl-32 pt-16 max-w-[16ch]'
				hidden = 'opacity-100'
			}}
			undo={() => {
				layout = ''
				headingClasses = ''
				hidden = 'opacity-0 hidden'
			}}
		>
			<div class="{layout} m-8 flex flex-col place-content-center place-items-center">
				<div class=" h-[70vh] w-[70vw] {hidden}">
					<PPAExample {stepNo} />
				</div>
			</div></Transition
		>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-center"
		out={() => {
			layout = 'h-[70vh]'
			visibility = 'hidden'
		}}
	>
		<Transition visible>
			<h1 class="text-4xl xl:text-7xl">Current limitations</h1>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			order={1}
			do={() => {
				grid_n_cols = 'grid-cols-1'
			}}
		>
			<div class="m-8 grid xl:m-16 {grid_n_cols} items-stretch gap-3">
				<Transition order={1} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-1')}>
					<div
						class="flex h-full max-w-[30vw] flex-col border-2 border-[var(--r-climate-rag-color)] bg-[var(--r-background-color)] p-4 xl:p-8"
					>
						<h2 class="mb-5 text-xl xl:text-2xl">LLMs</h2>
						<ul class="list-disc pl-5 text-left text-sm xl:text-xl">
							<li>LLMs occasionally hallucinate when sources don't contain enough information.</li>
							<li>Multi-modal LLMs not yet capable of parsing complex tables with colour keys.</li>
							<li>
								LLMs cannot handle large tables of data natively. Use of SQL/pandas queries may help
								here.
							</li>
							<li>
								LLMs not yet able to understand complex themes referenced across large documents. <a
									href="https://microsoft.github.io/graphrag/">Graph-based</a
								>
								<a href="https://github.com/HKUDS/LightRAG">solutions</a> may help here.
							</li>
						</ul>
						<img
							class="mt-auto mx-auto h-20 w-20 pt-5"
							alt="Vector database icon"
							src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmVyc2lvbj0iMS4xIgogICB2aWV3Qm94PSItNSAtMTAgODYuNDEwNjk4IDkzLjA3MzYwMSIKICAgaWQ9InN2ZzE2IgogICBzb2RpcG9kaTpkb2NuYW1lPSJub3VuLWNoYXRib3QtNjgzNTY0Ny5zdmciCiAgIHdpZHRoPSI4Ni40MTA2OTgiCiAgIGhlaWdodD0iOTMuMDczNjAxIgogICBpbmtzY2FwZTp2ZXJzaW9uPSIxLjIuMiAoYjBhODQ4NjU0MSwgMjAyMi0xMi0wMSkiCiAgIHhtbG5zOmlua3NjYXBlPSJodHRwOi8vd3d3Lmlua3NjYXBlLm9yZy9uYW1lc3BhY2VzL2lua3NjYXBlIgogICB4bWxuczpzb2RpcG9kaT0iaHR0cDovL3NvZGlwb2RpLnNvdXJjZWZvcmdlLm5ldC9EVEQvc29kaXBvZGktMC5kdGQiCiAgIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIKICAgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiAgPGRlZnMKICAgICBpZD0iZGVmczIwIiAvPgogIDxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3MTgiCiAgICAgcGFnZWNvbG9yPSIjZmZmZmZmIgogICAgIGJvcmRlcmNvbG9yPSIjNjY2NjY2IgogICAgIGJvcmRlcm9wYWNpdHk9IjEuMCIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9IjAiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIHNob3dncmlkPSJmYWxzZSIKICAgICBpbmtzY2FwZTp6b29tPSI2LjQ1MTg1MTkiCiAgICAgaW5rc2NhcGU6Y3g9IjQzLjMyMDg5NiIKICAgICBpbmtzY2FwZTpjeT0iNTQuMDE1NDk5IgogICAgIGlua3NjYXBlOndpbmRvdy13aWR0aD0iMTcyOCIKICAgICBpbmtzY2FwZTp3aW5kb3ctaGVpZ2h0PSIxMDQ4IgogICAgIGlua3NjYXBlOndpbmRvdy14PSIwIgogICAgIGlua3NjYXBlOndpbmRvdy15PSIzMiIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzE2IiAvPgogIDxnCiAgICAgaWQ9ImcxMCIKICAgICB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTEuNzgwMywtMTMuNDU3NCkiCiAgICAgc3R5bGU9ImZpbGw6I2UwMzEzMTtmaWxsLW9wYWNpdHk6MSI+CiAgICA8cGF0aAogICAgICAgZD0ibSA4Ny4yODEsNTIuMjExIHYgLTEyLjA3IGMgMCwtMy4yNSAtMi4zOTA2LC01Ljg5ODQgLTUuMzI4MSwtNS44OTg0IGggLTE4LjQ2OSBjIC0wLjgwMDc4LC02LjA3ODEgLTUuNjIxMSwtMTAuOTEgLTExLjcxMSwtMTEuNzExIHYgLTcuNTMxMiBjIDIuMzkwNiwtMC43NjE3MiA0LjE0MDYsLTIuOTY4OCA0LjE0MDYsLTUuNjIxMSAwLC0zLjI2OTUgLTIuNjQ4NCwtNS45MjE5IC01LjkyMTksLTUuOTIxOSAtMy4yNjk1LDAgLTUuOTIxOSwyLjY0ODQgLTUuOTIxOSw1LjkyMTkgMCwyLjY0ODQgMS43NSw0Ljg1OTQgNC4xNDA2LDUuNjIxMSB2IDcuNTMxMiBjIC02LjA3ODEsMC44MDA3OCAtMTAuOTEsNS42MjExIC0xMS43MTEsMTEuNzExIGggLTE4LjQ2OSBjIC0yLjk0MTQsMCAtNS4zMjgxLDIuNjQ4NCAtNS4zMjgxLDUuODk4NCB2IDEyLjA3IGMgLTMuMzkwNiwwLjgwMDc4IC01LjkyMTksMy44NTE2IC01LjkyMTksNy40ODA1IDAsMy42Mjg5IDIuNTMxMiw2LjY3MTkgNS45MjE5LDcuNDgwNSB2IDUuOTY4OCBjIDAsMi43MzA1IDEuNjkxNCw1LjAzOTEgMy45Njg4LDUuNjk5MiB2IDE3LjY5MSBsIDE0LjM0LC0xNy40ODggaCA1MC45MyBjIDIuOTQxNCwwIDUuMzI4MSwtMi42NDg0IDUuMzI4MSwtNS44OTg0IHYgLTUuOTY4OCBjIDMuMzkwNiwtMC44MDA3OCA1LjkyMTksLTMuODUxNiA1LjkyMTksLTcuNDgwNSAwLC0zLjYyODkgLTIuNTMxMiwtNi42NzE5IC01LjkyMTksLTcuNDgwNSB6IE0gMTIuNzE5LDYzLjQyMiBjIC0xLjM5MDYsLTAuNjcxODggLTIuMzcxMSwtMi4wNzgxIC0yLjM3MTEsLTMuNzMwNSAwLC0xLjY0ODQgMC45Njg3NSwtMy4wNTg2IDIuMzcxMSwtMy43MzA1IHogTSA1MCwyNS45NjEgYyA0Ljk0MTQsMCA5LjA1MDgsMy41NzgxIDkuODkwNiw4LjI4MTIgaCAtMTkuNzg5IGMgMC44Mzk4NCwtNC42OTkyIDQuOTQ5MiwtOC4yODEyIDkuODkwNiwtOC4yODEyIHogbSAzMy43Myw0Ny4xNjggYyAwLDEuMjY5NSAtMC44MDg1OSwyLjM1MTYgLTEuNzgxMiwyLjM1MTYgaCAtNTIuNTk4IGwgLTkuMTA5NCwxMS4xMDkgViA3NS40ODA2IEggMTguMDUgYyAtMC45NjA5NCwwIC0xLjc4MTIsLTEuMDc4MSAtMS43ODEyLC0yLjM1MTYgViA0MC4xNDEgYyAwLC0xLjI2OTUgMC44MDg1OSwtMi4zNTE2IDEuNzgxMiwtMi4zNTE2IGggNjMuOTEgYyAwLjk2MDk0LDAgMS43ODEyLDEuMDc4MSAxLjc4MTIsMi4zNTE2IHYgMzIuOTg4IHogbSAzLjU1MDgsLTkuNzA3IHYgLTcuNDQ5MiBjIDEuMzkwNiwwLjY3MTg4IDIuMzcxMSwyLjA3ODEgMi4zNzExLDMuNzMwNSAwLDEuNjQ4NCAtMC45Njg3NSwzLjA1ODYgLTIuMzcxMSwzLjczMDUgeiIKICAgICAgIGlkPSJwYXRoMiIKICAgICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgICA8cGF0aAogICAgICAgZD0ibSAzOC4xNzIsNDcuODUyIGMgMCwzLjk0NTMgLTUuOTIxOSwzLjk0NTMgLTUuOTIxOSwwIDAsLTMuOTQ5MiA1LjkyMTksLTMuOTQ5MiA1LjkyMTksMCIKICAgICAgIGlkPSJwYXRoNCIKICAgICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgICA8cGF0aAogICAgICAgZD0ibSA2Ny43NSw0Ny44NTIgYyAwLDMuOTQ1MyAtNS45MjE5LDMuOTQ1MyAtNS45MjE5LDAgMCwtMy45NDkyIDUuOTIxOSwtMy45NDkyIDUuOTIxOSwwIgogICAgICAgaWQ9InBhdGg2IgogICAgICAgc3R5bGU9ImZpbGw6I2UwMzEzMTtmaWxsLW9wYWNpdHk6MSIgLz4KICAgIDxwYXRoCiAgICAgICBkPSJtIDUwLDY4LjEyMSBjIDYuNTM5MSwwIDExLjgyOCwtNS4zMDA4IDExLjgyOCwtMTEuODI4IEggMzguMTU2IGMgMCw2LjUzOTEgNS4zMDA4LDExLjgyOCAxMS44MjgsMTEuODI4IHoiCiAgICAgICBpZD0icGF0aDgiCiAgICAgICBzdHlsZT0iZmlsbDojZTAzMTMxO2ZpbGwtb3BhY2l0eToxIiAvPgogIDwvZz4KPC9zdmc+Cg=="
						/>
					</div>
				</Transition>
				<Transition order={2} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-2')}>
					<div
						class="flex h-full max-w-[30vw] flex-col border-2 border-[var(--r-climate-rag-color)] bg-[var(--r-background-color)] p-4 xl:p-8"
					>
						<h2 class="mb-5 text-xl xl:text-2xl">Vector-based retrieval</h2>
						<ul class="list-disc pl-5 text-left text-sm xl:text-xl">
							<li>Vector databases are more expensive than traditional databases at scale</li>
							<li>
								Adopting improved embeddings models requires regenerating embeddings for entire
								database
							</li>
							<li>Techniques to embed images, charts and data still immature</li>
						</ul>
						<img
							class="mt-auto mx-auto h-20 w-20 pt-5"
							alt="Vector database icon"
							src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmVyc2lvbj0iMS4xIgogICB2aWV3Qm94PSItNSAtMTAgNzguNjkwNjk3IDgwLjAwMzQwMyIKICAgaWQ9InN2ZzgiCiAgIHNvZGlwb2RpOmRvY25hbWU9Im5vdW4tZGF0YS1zZWFyY2hpbmctNzI5ODk4Ny5zdmciCiAgIGlua3NjYXBlOnZlcnNpb249IjEuMi4yIChiMGE4NDg2NTQxLCAyMDIyLTEyLTAxKSIKICAgd2lkdGg9Ijc4LjY5MDY5NyIKICAgaGVpZ2h0PSI4MC4wMDM0MDMiCiAgIHhtbG5zOmlua3NjYXBlPSJodHRwOi8vd3d3Lmlua3NjYXBlLm9yZy9uYW1lc3BhY2VzL2lua3NjYXBlIgogICB4bWxuczpzb2RpcG9kaT0iaHR0cDovL3NvZGlwb2RpLnNvdXJjZWZvcmdlLm5ldC9EVEQvc29kaXBvZGktMC5kdGQiCiAgIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIKICAgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiAgPGRlZnMKICAgICBpZD0iZGVmczEyIiAvPgogIDxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3MTAiCiAgICAgcGFnZWNvbG9yPSIjZmZmZmZmIgogICAgIGJvcmRlcmNvbG9yPSIjNjY2NjY2IgogICAgIGJvcmRlcm9wYWNpdHk9IjEuMCIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9IjAiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIHNob3dncmlkPSJmYWxzZSIKICAgICBpbmtzY2FwZTp6b29tPSI2LjQ1MTg1MTkiCiAgICAgaW5rc2NhcGU6Y3g9IjI1Ljg4NDA0MSIKICAgICBpbmtzY2FwZTpjeT0iNjcuMDM1MDE3IgogICAgIGlua3NjYXBlOndpbmRvdy13aWR0aD0iMTcyOCIKICAgICBpbmtzY2FwZTp3aW5kb3ctaGVpZ2h0PSIxMDQ4IgogICAgIGlua3NjYXBlOndpbmRvdy14PSIwIgogICAgIGlua3NjYXBlOndpbmRvdy15PSIzMiIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzgiIC8+CiAgPHBhdGgKICAgICBkPSJtIDE4LjM4MzQwNiwxNi44ODYgYyAwLC0wLjcyNjU2IDAuNTg5ODQsLTEuMzE2NCAxLjMxNjQsLTEuMzE2NCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsMC41ODk4NCAxLjMxNjQsMS4zMTY0IDAsMC43MjY1NiAtMC41ODk4NCwxLjMxNjQgLTEuMzE2NCwxLjMxNjQgaCAtNS45NjQ4IGMgLTAuNzI2NTYsMCAtMS4zMTY0LC0wLjU4OTg0IC0xLjMxNjQsLTEuMzE2NCB6IG0gMS4zMjAzLDE3LjgyOCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsLTAuNTg5ODQgMS4zMTY0LC0xLjMxNjQgMCwtMC43MjY1NiAtMC41ODk4NCwtMS4zMTY0IC0xLjMxNjQsLTEuMzE2NCBoIC01Ljk2NDggYyAtMC43MjY1NiwwIC0xLjMxNjQsMC41ODk4NCAtMS4zMTY0LDEuMzE2NCAwLDAuNzI2NTYgMC41ODk4NCwxLjMxNjQgMS4zMTY0LDEuMzE2NCB6IG0gNS45NjA5LDEzLjg3OSBoIC01Ljk2NDggYyAtMC43MjY1NiwwIC0xLjMxNjQsMC41ODk4NCAtMS4zMTY0LDEuMzE2NCAwLDAuNzI2NTYgMC41ODk4NCwxLjMxNjQgMS4zMTY0LDEuMzE2NCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsLTAuNTg5ODQgMS4zMTY0LC0xLjMxNjQgMCwtMC43MjY1NiAtMC41ODk4NCwtMS4zMTY0IC0xLjMxNjQsLTEuMzE2NCB6IG0gNDguMDIzLDE2LjIxOSBjIC0wLjA0Mjk3LDEuNDIxOSAtMC42MjUsMi43MDcgLTEuNjQ0NSwzLjYyODkgLTEuMDU0NywxLjAzOTEgLTIuNDMzNiwxLjU2MjUgLTMuODEyNSwxLjU2MjUgLTEuMzkwNiwwIC0yLjc4MTIsLTAuNTI3MzQgLTMuODM5OCwtMS41ODk4IC0wLjM3ODkxLC0wLjM3ODkxIC0wLjc1MzkxLC0wLjc1IC0xLjExNzIsLTEuMTA5NCAtMy4zNzExLC0zLjMzOTggLTYuMDg5OCwtNi4wMzUyIC04Ljg2NzIsLTEwLjE0OCAtMi40MjU4LDEuMzI4MSAtNS4xMTcyLDIgLTcuODEyNSwyIC0yLjQyNTgsMCAtNC44NDc3LC0wLjU0Mjk3IC03LjA3ODEsLTEuNjIxMSAtNC43NzczLDEuMjU3OCAtMTAuNzI3LDEuOTQ5MiAtMTYuODI4LDEuOTQ5MiAtNy4xNzk3LDAgLTEzLjk0NSwtMC45MjU3OCAtMTkuMDU1LC0yLjYwMTYgLTUuNjQ0NSwtMS44NTE2IC04LjYyODksLTQuNDAyMyAtOC42Mjg5LC03LjM3MTEgbCAtMC4wMDM5LC00OS41MzUgYyAwLC0yLjk2ODggMi45ODQ0LC01LjUxOTUgOC42Mjg5LC03LjM3NSA1LjEwOTQsLTEuNjc5NyAxMS44NzUsLTIuNjAxNiAxOS4wNTUsLTIuNjAxNiA3LjE3OTcsMCAxMy45NDUsMC45MjU3OCAxOS4wNTUsMi42MDE2IDUuNjQ0NSwxLjg1NTUgOC42Mjg5LDQuNDAyMyA4LjYyODksNy4zNzUgdiAyNy4xODggYyAyLjgyMDMsMC42NzE4OCA1LjQ5NjEsMi4xMDE2IDcuNjk1Myw0LjMwMDggMy4wNjY0LDMuMDY2NCA0Ljc1MzksNy4xNDA2IDQuNzUzOSwxMS40NzMgMCwyLjc3NzMgLTAuNjk1MzEsNS40NDkyIC0yLDcuODE2NCA0LjEyMTEsMi43ODEyIDYuODIwMyw1LjUwMzkgMTAuMTY0LDguODc4OSAwLjM1NTQ3LDAuMzU5MzggMC43MTg3NSwwLjcyNjU2IDEuMDkzOCwxLjEwMTYgMS4wNzAzLDEuMDcwMyAxLjY2MDIsMi41NTg2IDEuNjEzMyw0LjA3ODEgeiBtIC03Ni4wNTUsLTY0LjgzNiBjIDAsMy4wNjI1IDkuNTMxMiw3LjMzOTggMjUuMDUxLDcuMzM5OCAxNS41MiwwIDI1LjA1MSwtNC4yNzM0IDI1LjA1MSwtNy4zMzk4IDAsLTMuMDYyNSAtOS41MzEyLC03LjM0MzggLTI1LjA1MSwtNy4zNDM4IC0xNS41MiwwIC0yNS4wNTEsNC4yNzczIC0yNS4wNTEsNy4zNDM4IHogbSAwLDE2LjUwOCBjIDAsMy4wNjY0IDkuNTMxMiw3LjM0MzggMjUuMDUxLDcuMzQzOCAxNS41MiwwIDI1LjA1MSwtNC4yNzczIDI1LjA1MSwtNy4zNDM4IFYgNC40MjkgYyAtMS40MzM2LDEuMDk3NyAtMy40NDE0LDIuMDc4MSAtNS45OTYxLDIuOTE4IC01LjEwOTQsMS42Nzk3IC0xMS44NzksMi42MDE2IC0xOS4wNTUsMi42MDE2IC03LjE3OTcsMCAtMTMuOTQ1LC0wLjkyNTc4IC0xOS4wNTUsLTIuNjAxNiAtMi41NTQ3LC0wLjgzOTg0IC00LjU1ODYsLTEuODIwMyAtNS45OTYxLC0yLjkxOCB6IG0gMCwxNi41MTIgYyAwLDMuMDYyNSA5LjUzMTIsNy4zMzk4IDI1LjA1MSw3LjMzOTggMi43MzA1LDAgNS40MDYyLC0wLjEzNjcyIDcuOTcyNywtMC40MDYyNSAwLjU4MjAzLC0zLjEwMTYgMi4wNjY0LC02LjA2NjQgNC40NjA5LC04LjQ2NDggMy40NTMxLC0zLjQ1MzEgOC4wODk4LC01LjAxNTYgMTIuNjE3LC00LjY5OTIgdiAtNS44MjQyIGMgLTEuNDMzNiwxLjA5NzcgLTMuNDQxNCwyLjA3ODEgLTUuOTk2MSwyLjkxOCAtNS4xMDk0LDEuNjc5NyAtMTEuODc1LDIuNjAxNiAtMTkuMDU1LDIuNjAxNiAtNy4xNzk3LDAgLTEzLjk0NSwtMC45MjU3OCAtMTkuMDU1LC0yLjYwMTYgLTIuNTU0NywtMC44Mzk4NCAtNC41NTg2LC0xLjgyMDMgLTUuOTk2MSwtMi45MTggeiBtIDM4Ljc1OCwyMi41NTkgYyAtMC40NDE0MSwtMC4zNTU0NyAtMC44NjcxOSwtMC43MzgyOCAtMS4yNzczLC0xLjE0NDUgLTMuMjQ2MSwtMy4yNSAtNC44MjAzLC03LjU0MyAtNC43MzQ0LC0xMS44MTIgLTIuNDg4MywwLjI0MjE5IC01LjA3MDMsMC4zNjcxOSAtNy42OTkyLDAuMzY3MTkgLTcuMTc5NywwIC0xMy45NDUsLTAuOTIxODggLTE5LjA1NSwtMi42MDE2IC0yLjU1NDcsLTAuODM5ODQgLTQuNTU4NiwtMS44MjAzIC01Ljk5NjEsLTIuOTE4IHYgMTIuMDU5IGMgMCwzLjA2MjUgOS41MzEyLDcuMzM5OCAyNS4wNTEsNy4zMzk4IDQuODcxMSwwIDkuNjI1LC0wLjQ1MzEyIDEzLjcwNywtMS4yODkxIHogbSAxOS44MDksLTMuMDA3OCBjIDIuNTY2NCwtMi41NjY0IDMuOTgwNSwtNS45ODA1IDMuOTgwNSwtOS42MDk0IDAsLTMuNjMyOCAtMS40MTQxLC03LjA0MyAtMy45ODA1LC05LjYwOTQgLTIuNjQ4NCwtMi42NDg0IC02LjEzMjgsLTMuOTc2NiAtOS42MDk0LC0zLjk3NjYgLTMuNDgwNSwwIC02Ljk2MDksMS4zMjQyIC05LjYwOTQsMy45NzY2IC01LjI5NjksNS4zMDA4IC01LjI5NjksMTMuOTIyIDAsMTkuMjIzIDIuNjQ4NCwyLjY0ODQgNi4xMjg5LDMuOTcyNyA5LjYwOTQsMy45NzI3IDMuNDgwNSwwIDYuOTYwOSwtMS4zMjQyIDkuNjEzMywtMy45NzI3IHogbSAwLjQwMjM0LDMuMTUyMyBjIDAuNTE5NTMsMC43NjU2MiAxLjAzNTIsMS40ODQ0IDEuNTU4NiwyLjE2NDEgbCAzLjM1OTQsLTMuMzU5NCBjIC0wLjY3OTY5LC0wLjUyMzQ0IC0xLjM5NDUsLTEuMDM5MSAtMi4xNjAyLC0xLjU1NDcgLTAuMzk4NDQsMC41MDc4MSAtMC44MzIwMywwLjk5NjA5IC0xLjI5NjksMS40NjA5IC0wLjQ2NDg3LDAuNDY0ODEgLTAuOTU3MDMsMC44OTQ1MyAtMS40NjA5LDEuMjg5MSB6IG0gMTQuNDUzLDkuMDM1MiBjIDAuMDIzNDQsLTAuNzk2ODggLTAuMjg1MTYsLTEuNTc4MSAtMC44NDc2NiwtMi4xNDA2IC0wLjM3ODkxLC0wLjM3ODkxIC0wLjc0MjE5LC0wLjc0NjA5IC0xLjA5NzcsLTEuMTA5NCAtMS45Mjk3LC0xLjk0OTIgLTMuNjQwNiwtMy42NzE5IC01LjUzNTIsLTUuMzA4NiBsIC0zLjczODMsMy43MzgzIGMgMS42Mjg5LDEuODg2NyAzLjM0NzcsMy41ODk4IDUuMjg5MSw1LjUxMTcgMC4zNjcxOSwwLjM2MzI4IDAuNzQyMTksMC43MzQzOCAxLjEyNSwxLjExNzIgMS4wOTM4LDEuMDkzOCAyLjg2NzIsMS4wOTM4IDMuOTU3LDAuMDAzOSAwLjAxOTUzLC0wLjAxOTUzIDAuMDM1MTYsLTAuMDM1MTYgMC4wNTQ2OSwtMC4wNTQ2OSAwLjQ4ODI4LC0wLjQzMzU5IDAuNzY5NTMsLTEuMDYyNSAwLjc4OTA2LC0xLjc2MTcgeiBtIC0xMi4xNDgsLTIxLjc5NyBjIDAsMy4yODkxIC0xLjI4MTIsNi4zODI4IC0zLjYwOTQsOC43MTA5IC0yLjMyODEsMi4zMjgxIC01LjQyMTksMy42MDk0IC04LjcxMDksMy42MDk0IC0zLjI4OTEsMCAtNi4zODI4LC0xLjI4MTIgLTguNzEwOSwtMy42MDk0IC0yLjMyODEsLTIuMzI4MSAtMy42MDk0LC01LjQyMTkgLTMuNjA5NCwtOC43MTA5IDAsLTMuMjg5IDEuMjgxMiwtNi4zODI4IDMuNjA5NCwtOC43MTA5IDIuMzI4MSwtMi4zMjgxIDUuNDIxOSwtMy42MDk0IDguNzEwOSwtMy42MDk0IDMuMjg5MSwwIDYuMzgyOCwxLjI4MTIgOC43MTA5LDMuNjA5NCAyLjMyODEsMi4zMjgxIDMuNjA5NCw1LjQyMTkgMy42MDk0LDguNzEwOSB6IG0gLTIuNjMyOCwwIGMgMCwtMi41ODU5IC0xLjAwNzgsLTUuMDE5NSAtMi44MzU5LC02Ljg0NzcgLTEuODI4MSwtMS44MjgyIC00LjI2MTcsLTIuODM1OSAtNi44NDc3LC0yLjgzNTkgLTIuNTg1OSwwIC01LjAxOTUsMS4wMDc4IC02Ljg0NzcsMi44MzU5IC0xLjgyODEsMS44MjgxIC0yLjgzNTksNC4yNjE3IC0yLjgzNTksNi44NDc3IDAsMi41ODYgMS4wMDc4LDUuMDE5NSAyLjgzNTksNi44NDc3IDEuODI4MSwxLjgyODEgNC4yNjE3LDIuODM1OSA2Ljg0NzcsMi44MzU5IDIuNTg1OSwwIDUuMDE5NSwtMS4wMDc4IDYuODQ3NywtMi44MzU5IDEuODI4MiwtMS44MjgxIDIuODM1OSwtNC4yNjE3IDIuODM1OSwtNi44NDc3IHoiCiAgICAgaWQ9InBhdGgyIgogICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+Cjwvc3ZnPgo="
						/>
					</div>
				</Transition>
				<Transition order={3} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-3')}>
					<div
						class="flex h-full max-w-[30vw] flex-col border-2 border-[var(--r-climate-rag-color)] bg-[var(--r-background-color)] p-4 xl:p-8"
					>
						<h2 class="mb-5 text-xl xl:text-2xl">Climate RAG pipeline</h2>
						<ul class="list-disc pl-5 text-left text-sm xl:text-xl">
							<li>Optimised for accuracy, not speed</li>
							<li>Data in plots and images are ignored (for now)</li>
							<li>
								Answering complex, multi-step questions requires manual orchestration (for now)
							</li>
							<li>
								For questions where the source of truth is known and in a structured format,
								classical data science techniques are more reliable.
							</li>
						</ul>
						<img
							class="mt-auto mx-auto h-20 w-20 pt-5"
							alt="Vector database icon"
							src="./logo-notext.svg"
						/>
					</div>
				</Transition>
			</div>
		</Transition>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-start"
		in={() => {
			headingClasses = ''
			layout = ''
		}}
		out={() => {
			layout = ''
		}}
	>
		<Transition
			visible
			enter="fade-enter"
			do={() => {
				headingClasses = ''
				hidden = 'opacity-0 hidden'
			}}
		>
			<h1 class="{headingClasses} static text-4xl !text-yellow-300 xl:text-7xl">
				Upcoming roadmap
			</h1>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			order={1}
			do={() => {
				layout = 'h-[70vh]'
				stepNo = 0
				headingClasses = 'text-left pl-32 pt-16 max-w-[16ch]'
				hidden = 'opacity-100'
			}}
			undo={() => {
				layout = ''
				headingClasses = ''
				hidden = 'opacity-0 hidden'
			}}
		>
			<div class="{layout} m-16 flex flex-col place-content-center place-items-center">
				<div class=" h-[100vh] w-[100vw] {hidden}">
					<Roadmap {stepNo} />
				</div>
			</div></Transition
		>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-start"
		in={() => {
			headingClasses = ''
			layout = ''
		}}
		out={() => {
			layout = 'h-[70vh]'
			headingClasses = 'text-left pt-16 pl-32 max-w-[16ch]'
			hidden = 'opacity-100'
			stepNo = 6
		}}
	>
		<Transition enter="blurry-enter" visible>
			<p class="text-4xl font-bold drop-shadow-sm xl:text-8xl">
				<img src="./logo.svg" alt="Climate RAG logo" class="w-96" />
			</p>
			<p class="max-w-[50ch] p-16 text-xl xl:text-3xl">
				Thanks for your interest! Climate-RAG is a work in progress. If you would like to try it
				out, check out the Github repository or contact <a
					href="https://bsky.app/profile/dldx.org"
					target="_blank">@dldx.org</a
				> to get access to a hosted instance.
			</p>
			<p class="mt-8 text-xl xl:text-3xl" style="font-family: var(--r-climate-rag-font)">
				<a class="btn" href="https://github.com/dldx/climate-rag" rel="noopener" target="_blank"
					><svg
						viewBox="0 0 16 16"
						width="32"
						height="32"
						class="octicon octicon-mark-github"
						style="fill: currentColor"
						aria-hidden="true"
						><path
							d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z"
						></path></svg
					>&nbsp;<span>Github</span></a
				>
			</p></Transition
		>
	</Slide>
</Presentation>

<style>
	.btn {
		display: inline-flex;
		padding: 0.5em 1em;
		margin: 0.5em;
		border: 1px solid var(--r-climate-rag-color);
		border-radius: 0.5em;
		background-color: #202020;
		color: white;
		text-decoration: none;
	}
	.btn:hover {
		box-shadow: 0 0 0 3px var(--r-climate-rag-color);
	}

	.btn:active {
		transform: translateY(1px);
	}
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
		transform: translateY(calc(var(--r-arrow-v-offset) / 2)) translateX(-1px); /* Center the arrow vertically */
		border-top: 10px solid transparent;
		border-bottom: 5px solid transparent;
		border-left: 10px solid white; /* Arrow color */
	}

	/* Set the large screen breakpoint */
	@media (min-width: 1280px) {
		.bubble::before {
			transform: translateY(var(--r-arrow-v-offset)) translateX(-1px); /* Center the arrow vertically */
			border-top: 20px solid transparent;
			border-bottom: 10px solid transparent;
			border-left: 20px solid white; /* Arrow color */
		}
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

	.highlighted-block {
		box-shadow: 10px 10px 0px 0px #bde352;
	}
	:global(.svelte-lightbox-footer) {
		text-align: center !important;
		font-family: var(--r-code-font) !important;
		padding-top: 1em !important;
	}
</style>
