<script lang="ts">
	import Switch from "./lib/Switch.svelte";

	const switches = $state([
		{ id: 1, checked: false, label: "Com" },
		{ id: 2, checked: false, label: "pro" },
		{ id: 3, checked: false, label: "mise" },
	]);

	function handleToggle(id: number) {
		const updated = switches.findIndex((s) => s.id === id);
		if (updated < 0) return;

		if (!switches[updated].checked) {
			const checked = switches.filter((s) => s.checked);

			if (checked.length >= 2) {
				const [first] = checked.toSorted((a, b) => a.id - b.id);
				first.checked = false;
			}
		}

		switches[updated].checked = !switches[updated].checked;
	}
</script>

<main class="min-h-screen flex flex-col items-center justify-center bg-neutral-50 gap-6">
	{#each switches as s (s.id)}
		<div class="flex items-center gap-4">
			<Switch onclick={() => handleToggle(s.id)} checked={s.checked} />

			<input
				class="focus-visible:outline-0 focus-visible:border-b focus-visible:border-neutral-900"
				type="text"
				bind:value={s.label}
			/>
		</div>
	{/each}
</main>
