<script lang="ts">
  import Roadmap from '$lib/Roadmap.svelte';

	import RagPipeline from '$lib/RagPipeline.svelte'
	import { Presentation, Slide, Code, Transition, Action } from '@animotion/core'
	import { tween } from '@animotion/motion'
	let text: HTMLParagraphElement
	let hidden = $state('hidden')
	let layout = $state('')
	let visibility = $state('')
	let stepNo = $state(0)
	let grid_n_cols = $state('grid-cols-1')
	let headingClasses = $state('')

	let randomNum = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1) + min)
	let imageToDisplay = $state('many-sources')
</script>

<Presentation
	options={{
		history: import.meta.env.VITE_DEV || false,
		transition: 'slide',
		controls: true,
		progress: true,
		width: 1920,
		height: 1080
	}}
>
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
	<Slide
		class="h-full place-content-center place-items-center"
		in={() => (layout = '')}
		out={() => {
			layout = ''
		}}
	>
		<Transition visible>
			<h1 class="static text-7xl !text-yellow-300">The Solution</h1>
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
					<RagPipeline {stepNo} />
				</Transition>
			</div>
		</Transition>
	</Slide>
	<Slide
		class="h-full place-content-center place-items-center"
		out={() => {
			layout = ''
			visibility = 'hidden'
		}}
	>
		<Transition visible>
			<h1 class="text-7xl">Current limitations</h1>
		</Transition>
		<Transition
			enter="fade-enter"
			class="hidden"
			order={1}
			do={() => {
				grid_n_cols = 'grid-cols-1'
			}}
		>
			<div class=" m-16 grid {grid_n_cols} items-stretch gap-3">
				<Transition order={1} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-1')}>
					<div
						class="flex h-full max-w-[20ch] flex-col border border-2 border-[#f46e72] bg-[var(--r-background-color)] p-8"
					>
						<h2 class="mb-5 text-2xl">LLMs</h2>
						<ul class="list-disc pl-5 text-left text-xl">
							<li>
								LLMs occasionally hallucinate when sources don't contain enough
								information.
							</li>
							<li>Multi-modal LLMs not yet capable of parsing complex tables with colour keys.</li>
							<li>
								LLMs cannot handle large tables of data natively. Use of SQL/pandas queries may help
								here.
							</li>
							<li>
								LLMs not yet able to understand complex themes referenced across large
								documents. <a href="https://microsoft.github.io/graphrag/">Graph-based</a>
								<a href="https://github.com/HKUDS/LightRAG">solutions</a> may help here.
							</li>
						</ul>
						<img
							class="mt-auto mx-auto h-20 w-20"
							alt="Vector database icon"
							src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmVyc2lvbj0iMS4xIgogICB2aWV3Qm94PSItNSAtMTAgODYuNDEwNjk4IDkzLjA3MzYwMSIKICAgaWQ9InN2ZzE2IgogICBzb2RpcG9kaTpkb2NuYW1lPSJub3VuLWNoYXRib3QtNjgzNTY0Ny5zdmciCiAgIHdpZHRoPSI4Ni40MTA2OTgiCiAgIGhlaWdodD0iOTMuMDczNjAxIgogICBpbmtzY2FwZTp2ZXJzaW9uPSIxLjIuMiAoYjBhODQ4NjU0MSwgMjAyMi0xMi0wMSkiCiAgIHhtbG5zOmlua3NjYXBlPSJodHRwOi8vd3d3Lmlua3NjYXBlLm9yZy9uYW1lc3BhY2VzL2lua3NjYXBlIgogICB4bWxuczpzb2RpcG9kaT0iaHR0cDovL3NvZGlwb2RpLnNvdXJjZWZvcmdlLm5ldC9EVEQvc29kaXBvZGktMC5kdGQiCiAgIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIKICAgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiAgPGRlZnMKICAgICBpZD0iZGVmczIwIiAvPgogIDxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3MTgiCiAgICAgcGFnZWNvbG9yPSIjZmZmZmZmIgogICAgIGJvcmRlcmNvbG9yPSIjNjY2NjY2IgogICAgIGJvcmRlcm9wYWNpdHk9IjEuMCIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9IjAiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIHNob3dncmlkPSJmYWxzZSIKICAgICBpbmtzY2FwZTp6b29tPSI2LjQ1MTg1MTkiCiAgICAgaW5rc2NhcGU6Y3g9IjQzLjMyMDg5NiIKICAgICBpbmtzY2FwZTpjeT0iNTQuMDE1NDk5IgogICAgIGlua3NjYXBlOndpbmRvdy13aWR0aD0iMTcyOCIKICAgICBpbmtzY2FwZTp3aW5kb3ctaGVpZ2h0PSIxMDQ4IgogICAgIGlua3NjYXBlOndpbmRvdy14PSIwIgogICAgIGlua3NjYXBlOndpbmRvdy15PSIzMiIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzE2IiAvPgogIDxnCiAgICAgaWQ9ImcxMCIKICAgICB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTEuNzgwMywtMTMuNDU3NCkiCiAgICAgc3R5bGU9ImZpbGw6I2UwMzEzMTtmaWxsLW9wYWNpdHk6MSI+CiAgICA8cGF0aAogICAgICAgZD0ibSA4Ny4yODEsNTIuMjExIHYgLTEyLjA3IGMgMCwtMy4yNSAtMi4zOTA2LC01Ljg5ODQgLTUuMzI4MSwtNS44OTg0IGggLTE4LjQ2OSBjIC0wLjgwMDc4LC02LjA3ODEgLTUuNjIxMSwtMTAuOTEgLTExLjcxMSwtMTEuNzExIHYgLTcuNTMxMiBjIDIuMzkwNiwtMC43NjE3MiA0LjE0MDYsLTIuOTY4OCA0LjE0MDYsLTUuNjIxMSAwLC0zLjI2OTUgLTIuNjQ4NCwtNS45MjE5IC01LjkyMTksLTUuOTIxOSAtMy4yNjk1LDAgLTUuOTIxOSwyLjY0ODQgLTUuOTIxOSw1LjkyMTkgMCwyLjY0ODQgMS43NSw0Ljg1OTQgNC4xNDA2LDUuNjIxMSB2IDcuNTMxMiBjIC02LjA3ODEsMC44MDA3OCAtMTAuOTEsNS42MjExIC0xMS43MTEsMTEuNzExIGggLTE4LjQ2OSBjIC0yLjk0MTQsMCAtNS4zMjgxLDIuNjQ4NCAtNS4zMjgxLDUuODk4NCB2IDEyLjA3IGMgLTMuMzkwNiwwLjgwMDc4IC01LjkyMTksMy44NTE2IC01LjkyMTksNy40ODA1IDAsMy42Mjg5IDIuNTMxMiw2LjY3MTkgNS45MjE5LDcuNDgwNSB2IDUuOTY4OCBjIDAsMi43MzA1IDEuNjkxNCw1LjAzOTEgMy45Njg4LDUuNjk5MiB2IDE3LjY5MSBsIDE0LjM0LC0xNy40ODggaCA1MC45MyBjIDIuOTQxNCwwIDUuMzI4MSwtMi42NDg0IDUuMzI4MSwtNS44OTg0IHYgLTUuOTY4OCBjIDMuMzkwNiwtMC44MDA3OCA1LjkyMTksLTMuODUxNiA1LjkyMTksLTcuNDgwNSAwLC0zLjYyODkgLTIuNTMxMiwtNi42NzE5IC01LjkyMTksLTcuNDgwNSB6IE0gMTIuNzE5LDYzLjQyMiBjIC0xLjM5MDYsLTAuNjcxODggLTIuMzcxMSwtMi4wNzgxIC0yLjM3MTEsLTMuNzMwNSAwLC0xLjY0ODQgMC45Njg3NSwtMy4wNTg2IDIuMzcxMSwtMy43MzA1IHogTSA1MCwyNS45NjEgYyA0Ljk0MTQsMCA5LjA1MDgsMy41NzgxIDkuODkwNiw4LjI4MTIgaCAtMTkuNzg5IGMgMC44Mzk4NCwtNC42OTkyIDQuOTQ5MiwtOC4yODEyIDkuODkwNiwtOC4yODEyIHogbSAzMy43Myw0Ny4xNjggYyAwLDEuMjY5NSAtMC44MDg1OSwyLjM1MTYgLTEuNzgxMiwyLjM1MTYgaCAtNTIuNTk4IGwgLTkuMTA5NCwxMS4xMDkgViA3NS40ODA2IEggMTguMDUgYyAtMC45NjA5NCwwIC0xLjc4MTIsLTEuMDc4MSAtMS43ODEyLC0yLjM1MTYgViA0MC4xNDEgYyAwLC0xLjI2OTUgMC44MDg1OSwtMi4zNTE2IDEuNzgxMiwtMi4zNTE2IGggNjMuOTEgYyAwLjk2MDk0LDAgMS43ODEyLDEuMDc4MSAxLjc4MTIsMi4zNTE2IHYgMzIuOTg4IHogbSAzLjU1MDgsLTkuNzA3IHYgLTcuNDQ5MiBjIDEuMzkwNiwwLjY3MTg4IDIuMzcxMSwyLjA3ODEgMi4zNzExLDMuNzMwNSAwLDEuNjQ4NCAtMC45Njg3NSwzLjA1ODYgLTIuMzcxMSwzLjczMDUgeiIKICAgICAgIGlkPSJwYXRoMiIKICAgICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgICA8cGF0aAogICAgICAgZD0ibSAzOC4xNzIsNDcuODUyIGMgMCwzLjk0NTMgLTUuOTIxOSwzLjk0NTMgLTUuOTIxOSwwIDAsLTMuOTQ5MiA1LjkyMTksLTMuOTQ5MiA1LjkyMTksMCIKICAgICAgIGlkPSJwYXRoNCIKICAgICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgICA8cGF0aAogICAgICAgZD0ibSA2Ny43NSw0Ny44NTIgYyAwLDMuOTQ1MyAtNS45MjE5LDMuOTQ1MyAtNS45MjE5LDAgMCwtMy45NDkyIDUuOTIxOSwtMy45NDkyIDUuOTIxOSwwIgogICAgICAgaWQ9InBhdGg2IgogICAgICAgc3R5bGU9ImZpbGw6I2UwMzEzMTtmaWxsLW9wYWNpdHk6MSIgLz4KICAgIDxwYXRoCiAgICAgICBkPSJtIDUwLDY4LjEyMSBjIDYuNTM5MSwwIDExLjgyOCwtNS4zMDA4IDExLjgyOCwtMTEuODI4IEggMzguMTU2IGMgMCw2LjUzOTEgNS4zMDA4LDExLjgyOCAxMS44MjgsMTEuODI4IHoiCiAgICAgICBpZD0icGF0aDgiCiAgICAgICBzdHlsZT0iZmlsbDojZTAzMTMxO2ZpbGwtb3BhY2l0eToxIiAvPgogIDwvZz4KPC9zdmc+Cg=="
						/>
					</div>
				</Transition>
				<Transition order={2} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-2')}>
					<div
						class="flex h-full max-w-[20ch] flex-col border border-2 border-[#f46e72] bg-[var(--r-background-color)] p-8"
					>
						<h2 class="mb-5 text-2xl">Vector-based retrieval</h2>
						<ul class="list-disc pl-5 text-left text-xl">
							<li>Vector databases are more expensive than traditional databases at scale</li>
							<li>
								Adopting improved embeddings models requires regenerating embeddings for entire
								database
							</li>
							<li>Techniques to embed images, charts and data still immature</li>
						</ul>
						<img
							class="mt-auto mx-auto h-20 w-20"
							alt="Vector database icon"
							src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmVyc2lvbj0iMS4xIgogICB2aWV3Qm94PSItNSAtMTAgNzguNjkwNjk3IDgwLjAwMzQwMyIKICAgaWQ9InN2ZzgiCiAgIHNvZGlwb2RpOmRvY25hbWU9Im5vdW4tZGF0YS1zZWFyY2hpbmctNzI5ODk4Ny5zdmciCiAgIGlua3NjYXBlOnZlcnNpb249IjEuMi4yIChiMGE4NDg2NTQxLCAyMDIyLTEyLTAxKSIKICAgd2lkdGg9Ijc4LjY5MDY5NyIKICAgaGVpZ2h0PSI4MC4wMDM0MDMiCiAgIHhtbG5zOmlua3NjYXBlPSJodHRwOi8vd3d3Lmlua3NjYXBlLm9yZy9uYW1lc3BhY2VzL2lua3NjYXBlIgogICB4bWxuczpzb2RpcG9kaT0iaHR0cDovL3NvZGlwb2RpLnNvdXJjZWZvcmdlLm5ldC9EVEQvc29kaXBvZGktMC5kdGQiCiAgIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIKICAgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiAgPGRlZnMKICAgICBpZD0iZGVmczEyIiAvPgogIDxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3MTAiCiAgICAgcGFnZWNvbG9yPSIjZmZmZmZmIgogICAgIGJvcmRlcmNvbG9yPSIjNjY2NjY2IgogICAgIGJvcmRlcm9wYWNpdHk9IjEuMCIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9IjAiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIHNob3dncmlkPSJmYWxzZSIKICAgICBpbmtzY2FwZTp6b29tPSI2LjQ1MTg1MTkiCiAgICAgaW5rc2NhcGU6Y3g9IjI1Ljg4NDA0MSIKICAgICBpbmtzY2FwZTpjeT0iNjcuMDM1MDE3IgogICAgIGlua3NjYXBlOndpbmRvdy13aWR0aD0iMTcyOCIKICAgICBpbmtzY2FwZTp3aW5kb3ctaGVpZ2h0PSIxMDQ4IgogICAgIGlua3NjYXBlOndpbmRvdy14PSIwIgogICAgIGlua3NjYXBlOndpbmRvdy15PSIzMiIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzgiIC8+CiAgPHBhdGgKICAgICBkPSJtIDE4LjM4MzQwNiwxNi44ODYgYyAwLC0wLjcyNjU2IDAuNTg5ODQsLTEuMzE2NCAxLjMxNjQsLTEuMzE2NCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsMC41ODk4NCAxLjMxNjQsMS4zMTY0IDAsMC43MjY1NiAtMC41ODk4NCwxLjMxNjQgLTEuMzE2NCwxLjMxNjQgaCAtNS45NjQ4IGMgLTAuNzI2NTYsMCAtMS4zMTY0LC0wLjU4OTg0IC0xLjMxNjQsLTEuMzE2NCB6IG0gMS4zMjAzLDE3LjgyOCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsLTAuNTg5ODQgMS4zMTY0LC0xLjMxNjQgMCwtMC43MjY1NiAtMC41ODk4NCwtMS4zMTY0IC0xLjMxNjQsLTEuMzE2NCBoIC01Ljk2NDggYyAtMC43MjY1NiwwIC0xLjMxNjQsMC41ODk4NCAtMS4zMTY0LDEuMzE2NCAwLDAuNzI2NTYgMC41ODk4NCwxLjMxNjQgMS4zMTY0LDEuMzE2NCB6IG0gNS45NjA5LDEzLjg3OSBoIC01Ljk2NDggYyAtMC43MjY1NiwwIC0xLjMxNjQsMC41ODk4NCAtMS4zMTY0LDEuMzE2NCAwLDAuNzI2NTYgMC41ODk4NCwxLjMxNjQgMS4zMTY0LDEuMzE2NCBoIDUuOTY0OCBjIDAuNzI2NTYsMCAxLjMxNjQsLTAuNTg5ODQgMS4zMTY0LC0xLjMxNjQgMCwtMC43MjY1NiAtMC41ODk4NCwtMS4zMTY0IC0xLjMxNjQsLTEuMzE2NCB6IG0gNDguMDIzLDE2LjIxOSBjIC0wLjA0Mjk3LDEuNDIxOSAtMC42MjUsMi43MDcgLTEuNjQ0NSwzLjYyODkgLTEuMDU0NywxLjAzOTEgLTIuNDMzNiwxLjU2MjUgLTMuODEyNSwxLjU2MjUgLTEuMzkwNiwwIC0yLjc4MTIsLTAuNTI3MzQgLTMuODM5OCwtMS41ODk4IC0wLjM3ODkxLC0wLjM3ODkxIC0wLjc1MzkxLC0wLjc1IC0xLjExNzIsLTEuMTA5NCAtMy4zNzExLC0zLjMzOTggLTYuMDg5OCwtNi4wMzUyIC04Ljg2NzIsLTEwLjE0OCAtMi40MjU4LDEuMzI4MSAtNS4xMTcyLDIgLTcuODEyNSwyIC0yLjQyNTgsMCAtNC44NDc3LC0wLjU0Mjk3IC03LjA3ODEsLTEuNjIxMSAtNC43NzczLDEuMjU3OCAtMTAuNzI3LDEuOTQ5MiAtMTYuODI4LDEuOTQ5MiAtNy4xNzk3LDAgLTEzLjk0NSwtMC45MjU3OCAtMTkuMDU1LC0yLjYwMTYgLTUuNjQ0NSwtMS44NTE2IC04LjYyODksLTQuNDAyMyAtOC42Mjg5LC03LjM3MTEgbCAtMC4wMDM5LC00OS41MzUgYyAwLC0yLjk2ODggMi45ODQ0LC01LjUxOTUgOC42Mjg5LC03LjM3NSA1LjEwOTQsLTEuNjc5NyAxMS44NzUsLTIuNjAxNiAxOS4wNTUsLTIuNjAxNiA3LjE3OTcsMCAxMy45NDUsMC45MjU3OCAxOS4wNTUsMi42MDE2IDUuNjQ0NSwxLjg1NTUgOC42Mjg5LDQuNDAyMyA4LjYyODksNy4zNzUgdiAyNy4xODggYyAyLjgyMDMsMC42NzE4OCA1LjQ5NjEsMi4xMDE2IDcuNjk1Myw0LjMwMDggMy4wNjY0LDMuMDY2NCA0Ljc1MzksNy4xNDA2IDQuNzUzOSwxMS40NzMgMCwyLjc3NzMgLTAuNjk1MzEsNS40NDkyIC0yLDcuODE2NCA0LjEyMTEsMi43ODEyIDYuODIwMyw1LjUwMzkgMTAuMTY0LDguODc4OSAwLjM1NTQ3LDAuMzU5MzggMC43MTg3NSwwLjcyNjU2IDEuMDkzOCwxLjEwMTYgMS4wNzAzLDEuMDcwMyAxLjY2MDIsMi41NTg2IDEuNjEzMyw0LjA3ODEgeiBtIC03Ni4wNTUsLTY0LjgzNiBjIDAsMy4wNjI1IDkuNTMxMiw3LjMzOTggMjUuMDUxLDcuMzM5OCAxNS41MiwwIDI1LjA1MSwtNC4yNzM0IDI1LjA1MSwtNy4zMzk4IDAsLTMuMDYyNSAtOS41MzEyLC03LjM0MzggLTI1LjA1MSwtNy4zNDM4IC0xNS41MiwwIC0yNS4wNTEsNC4yNzczIC0yNS4wNTEsNy4zNDM4IHogbSAwLDE2LjUwOCBjIDAsMy4wNjY0IDkuNTMxMiw3LjM0MzggMjUuMDUxLDcuMzQzOCAxNS41MiwwIDI1LjA1MSwtNC4yNzczIDI1LjA1MSwtNy4zNDM4IFYgNC40MjkgYyAtMS40MzM2LDEuMDk3NyAtMy40NDE0LDIuMDc4MSAtNS45OTYxLDIuOTE4IC01LjEwOTQsMS42Nzk3IC0xMS44NzksMi42MDE2IC0xOS4wNTUsMi42MDE2IC03LjE3OTcsMCAtMTMuOTQ1LC0wLjkyNTc4IC0xOS4wNTUsLTIuNjAxNiAtMi41NTQ3LC0wLjgzOTg0IC00LjU1ODYsLTEuODIwMyAtNS45OTYxLC0yLjkxOCB6IG0gMCwxNi41MTIgYyAwLDMuMDYyNSA5LjUzMTIsNy4zMzk4IDI1LjA1MSw3LjMzOTggMi43MzA1LDAgNS40MDYyLC0wLjEzNjcyIDcuOTcyNywtMC40MDYyNSAwLjU4MjAzLC0zLjEwMTYgMi4wNjY0LC02LjA2NjQgNC40NjA5LC04LjQ2NDggMy40NTMxLC0zLjQ1MzEgOC4wODk4LC01LjAxNTYgMTIuNjE3LC00LjY5OTIgdiAtNS44MjQyIGMgLTEuNDMzNiwxLjA5NzcgLTMuNDQxNCwyLjA3ODEgLTUuOTk2MSwyLjkxOCAtNS4xMDk0LDEuNjc5NyAtMTEuODc1LDIuNjAxNiAtMTkuMDU1LDIuNjAxNiAtNy4xNzk3LDAgLTEzLjk0NSwtMC45MjU3OCAtMTkuMDU1LC0yLjYwMTYgLTIuNTU0NywtMC44Mzk4NCAtNC41NTg2LC0xLjgyMDMgLTUuOTk2MSwtMi45MTggeiBtIDM4Ljc1OCwyMi41NTkgYyAtMC40NDE0MSwtMC4zNTU0NyAtMC44NjcxOSwtMC43MzgyOCAtMS4yNzczLC0xLjE0NDUgLTMuMjQ2MSwtMy4yNSAtNC44MjAzLC03LjU0MyAtNC43MzQ0LC0xMS44MTIgLTIuNDg4MywwLjI0MjE5IC01LjA3MDMsMC4zNjcxOSAtNy42OTkyLDAuMzY3MTkgLTcuMTc5NywwIC0xMy45NDUsLTAuOTIxODggLTE5LjA1NSwtMi42MDE2IC0yLjU1NDcsLTAuODM5ODQgLTQuNTU4NiwtMS44MjAzIC01Ljk5NjEsLTIuOTE4IHYgMTIuMDU5IGMgMCwzLjA2MjUgOS41MzEyLDcuMzM5OCAyNS4wNTEsNy4zMzk4IDQuODcxMSwwIDkuNjI1LC0wLjQ1MzEyIDEzLjcwNywtMS4yODkxIHogbSAxOS44MDksLTMuMDA3OCBjIDIuNTY2NCwtMi41NjY0IDMuOTgwNSwtNS45ODA1IDMuOTgwNSwtOS42MDk0IDAsLTMuNjMyOCAtMS40MTQxLC03LjA0MyAtMy45ODA1LC05LjYwOTQgLTIuNjQ4NCwtMi42NDg0IC02LjEzMjgsLTMuOTc2NiAtOS42MDk0LC0zLjk3NjYgLTMuNDgwNSwwIC02Ljk2MDksMS4zMjQyIC05LjYwOTQsMy45NzY2IC01LjI5NjksNS4zMDA4IC01LjI5NjksMTMuOTIyIDAsMTkuMjIzIDIuNjQ4NCwyLjY0ODQgNi4xMjg5LDMuOTcyNyA5LjYwOTQsMy45NzI3IDMuNDgwNSwwIDYuOTYwOSwtMS4zMjQyIDkuNjEzMywtMy45NzI3IHogbSAwLjQwMjM0LDMuMTUyMyBjIDAuNTE5NTMsMC43NjU2MiAxLjAzNTIsMS40ODQ0IDEuNTU4NiwyLjE2NDEgbCAzLjM1OTQsLTMuMzU5NCBjIC0wLjY3OTY5LC0wLjUyMzQ0IC0xLjM5NDUsLTEuMDM5MSAtMi4xNjAyLC0xLjU1NDcgLTAuMzk4NDQsMC41MDc4MSAtMC44MzIwMywwLjk5NjA5IC0xLjI5NjksMS40NjA5IC0wLjQ2NDg3LDAuNDY0ODEgLTAuOTU3MDMsMC44OTQ1MyAtMS40NjA5LDEuMjg5MSB6IG0gMTQuNDUzLDkuMDM1MiBjIDAuMDIzNDQsLTAuNzk2ODggLTAuMjg1MTYsLTEuNTc4MSAtMC44NDc2NiwtMi4xNDA2IC0wLjM3ODkxLC0wLjM3ODkxIC0wLjc0MjE5LC0wLjc0NjA5IC0xLjA5NzcsLTEuMTA5NCAtMS45Mjk3LC0xLjk0OTIgLTMuNjQwNiwtMy42NzE5IC01LjUzNTIsLTUuMzA4NiBsIC0zLjczODMsMy43MzgzIGMgMS42Mjg5LDEuODg2NyAzLjM0NzcsMy41ODk4IDUuMjg5MSw1LjUxMTcgMC4zNjcxOSwwLjM2MzI4IDAuNzQyMTksMC43MzQzOCAxLjEyNSwxLjExNzIgMS4wOTM4LDEuMDkzOCAyLjg2NzIsMS4wOTM4IDMuOTU3LDAuMDAzOSAwLjAxOTUzLC0wLjAxOTUzIDAuMDM1MTYsLTAuMDM1MTYgMC4wNTQ2OSwtMC4wNTQ2OSAwLjQ4ODI4LC0wLjQzMzU5IDAuNzY5NTMsLTEuMDYyNSAwLjc4OTA2LC0xLjc2MTcgeiBtIC0xMi4xNDgsLTIxLjc5NyBjIDAsMy4yODkxIC0xLjI4MTIsNi4zODI4IC0zLjYwOTQsOC43MTA5IC0yLjMyODEsMi4zMjgxIC01LjQyMTksMy42MDk0IC04LjcxMDksMy42MDk0IC0zLjI4OTEsMCAtNi4zODI4LC0xLjI4MTIgLTguNzEwOSwtMy42MDk0IC0yLjMyODEsLTIuMzI4MSAtMy42MDk0LC01LjQyMTkgLTMuNjA5NCwtOC43MTA5IDAsLTMuMjg5IDEuMjgxMiwtNi4zODI4IDMuNjA5NCwtOC43MTA5IDIuMzI4MSwtMi4zMjgxIDUuNDIxOSwtMy42MDk0IDguNzEwOSwtMy42MDk0IDMuMjg5MSwwIDYuMzgyOCwxLjI4MTIgOC43MTA5LDMuNjA5NCAyLjMyODEsMi4zMjgxIDMuNjA5NCw1LjQyMTkgMy42MDk0LDguNzEwOSB6IG0gLTIuNjMyOCwwIGMgMCwtMi41ODU5IC0xLjAwNzgsLTUuMDE5NSAtMi44MzU5LC02Ljg0NzcgLTEuODI4MSwtMS44MjgyIC00LjI2MTcsLTIuODM1OSAtNi44NDc3LC0yLjgzNTkgLTIuNTg1OSwwIC01LjAxOTUsMS4wMDc4IC02Ljg0NzcsMi44MzU5IC0xLjgyODEsMS44MjgxIC0yLjgzNTksNC4yNjE3IC0yLjgzNTksNi44NDc3IDAsMi41ODYgMS4wMDc4LDUuMDE5NSAyLjgzNTksNi44NDc3IDEuODI4MSwxLjgyODEgNC4yNjE3LDIuODM1OSA2Ljg0NzcsMi44MzU5IDIuNTg1OSwwIDUuMDE5NSwtMS4wMDc4IDYuODQ3NywtMi44MzU5IDEuODI4MiwtMS44MjgxIDIuODM1OSwtNC4yNjE3IDIuODM1OSwtNi44NDc3IHoiCiAgICAgaWQ9InBhdGgyIgogICAgIHN0eWxlPSJmaWxsOiNlMDMxMzE7ZmlsbC1vcGFjaXR5OjEiIC8+Cjwvc3ZnPgo="
						/>
					</div>
				</Transition>
				<Transition order={3} enter="fade-enter" do={() => (grid_n_cols = 'grid-cols-3')}>
					<div
						class="flex h-full max-w-[20ch] flex-col border border-2 border-[var(--r-climate-rag-color)] bg-[var(--r-background-color)] p-8"
					>
						<h2 class="mb-5 text-2xl">Climate-RAG pipeline</h2>
						<ul class="list-disc pl-5 text-left text-xl">
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
							class="mt-auto mx-auto h-20 w-20"
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
		<Transition visible enter="fade-enter"
		do={() => {
			headingClasses = ""
			hidden = "opacity-0 hidden"
		}}
		>
			<h1 class="{headingClasses} static text-7xl !text-yellow-300">Upcoming roadmap</h1>
			</Transition>
			<Transition
			enter="fade-enter"
			class="hidden"
			order={1}
			do={() => {
				layout = 'h-[600px]'
				stepNo = 0
				headingClasses = "text-left pl-32 max-w-[16ch]"
			hidden = "opacity-100"
			}}
			undo={() => {
				layout = ''
				headingClasses = ''
				hidden = "opacity-0 hidden"
			}}
		>
			<div class="{layout} m-16 flex flex-col place-content-center place-items-center">
				<div class=" h-[100vh] w-[100vw] {hidden}">
<Roadmap {stepNo} />
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
				layout = 'h-[600px]'
				headingClasses = "text-left pl-32 max-w-[16ch]"
			hidden = "opacity-100"
		}}
	>
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
