<script lang="ts">
	let { oncreate, onclose } = $props<{
		oncreate: (event: CustomEvent<{ title: string }>) => void;
		onclose: () => void;
	}>();

	let title = $state('');

	function handleSubmit(event: SubmitEvent) {
		event.preventDefault();
		if (!title.trim()) return;

		oncreate(new CustomEvent('create', { detail: { title } }));
	}
</script>

<div class="fixed inset-0 z-50 flex items-center justify-center bg-[#0d0f12] p-4 backdrop-blur-sm">
	<div class="w-full max-w-md rounded-2xl border border-white/[0.09] bg-[#0d0f12] p-6 shadow-xl">
		<h2 class="mb-4 text-xl font-bold text-white">Create New Project</h2>

		<form onsubmit={handleSubmit}>
			<div class="mb-4">
				<label for="new-project-title" class="mb-1.5 block text-xs font-semibold text-white/60"
					>Project Title</label
				>
				<input
					id="new-project-title"
					type="text"
					placeholder="My awesome project..."
					bind:value={title}
					required
					class="w-full rounded-xl border border-white/10 bg-white/[0.03] px-3 py-2.5 text-sm transition-all placeholder:text-white/30 focus:border-transparent focus:ring-2 focus:ring-slate-900 focus:outline-none"
				/>
			</div>

			<div class="flex justify-end gap-2">
				<button
					type="button"
					onclick={onclose}
					class="rounded-xl border border-white/10 bg-white/[0.03] px-4 py-2 text-sm font-medium text-white/60 transition-colors hover:bg-white/[0.06]"
				>
					Cancel
				</button>
				<button
					type="submit"
					class="rounded-xl bg-linear-to-b from-[#4fb3f7] to-[#1c6ba3] px-4 py-2 text-sm font-medium text-white shadow-sm transition-colors hover:bg-slate-800 hover:shadow-[0_6px_26px_-4px_rgba(63,169,245,1)]"
				>
					Create Project
				</button>
			</div>
		</form>
	</div>
</div>
