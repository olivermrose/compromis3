<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";
	import { Spring } from "svelte/motion";

	let { checked, onclick }: { checked: boolean } & HTMLAttributes<HTMLButtonElement> = $props();

	const x = new Spring(0, {
		stiffness: 0.25,
		damping: 0.55,
	});

	$effect(() => {
		x.target = checked ? 16 : 0;
	});
</script>

<button
	class="flex items-center w-12 h-7.5 p-1 rounded-full bg-[#ddd] hover:cursor-pointer aria-checked:bg-[#4bd763]"
	type="button"
	role="switch"
	aria-checked={checked}
	aria-label="Switch"
	{onclick}
>
	<span
		class="size-6 rounded-full bg-white shadow-md translate-x-(--x)"
		style:--x="{x.current}px"
	></span>
</button>
