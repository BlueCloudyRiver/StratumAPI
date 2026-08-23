<script lang="ts">
	import { logout, API, getAuthHeader } from '$lib/api';
	import { redirect } from '@sveltejs/kit';

	let { active = '' }: { active?: 'dashboard' | 'clients' | 'members' | 'workspaces' | '' } =
		$props();

	/*
	let input = $state('');
	let subInput = $derived(input.trim());

	async function searchWorkspaces() {
		const auth = getAuthHeader();

		if (!auth) throw new Error('Failed to get authoriation details');
		try {
			const resp = await fetch(`${API}/workspaces?query=${subInput}`, {
				method: 'GET',
				headers: auth
			});
			if (!resp.ok) throw new Error('Failed to fetch workspaces');
		} catch (err) {
			console.error('Failed to search workspaces: ', err);
		}
	}
	*/
	const links: { href: string; label: string; key: string }[] = [
		{ href: '/dashboard', label: 'Dashboard', key: 'dashboard' },
		{ href: '/clients', label: 'Clients', key: 'clients' },
		{ href: '/members', label: 'Members', key: 'members' },
		{ href: '/workspaces', label: 'Workspaces', key: 'workspaces' }
	];
</script>

<nav class="sticky top-0 z-30 border-b border-white/[0.09] bg-[#08090b]/55 backdrop-blur-xl">
	<div class="mx-auto flex max-w-6xl items-center justify-between px-6 py-[18px]">
		<a href="/dashboard" class="flex items-center gap-2.5">
			<svg
				width="20"
				height="20"
				viewBox="0 0 24 24"
				fill="none"
				stroke="#5db9f7"
				stroke-width="1.8"
				><polygon points="12 2 2 7 12 12 22 7 12 2" /><polyline
					points="2 17 12 22 22 17"
				/><polyline points="2 12 12 17 22 12" /></svg
			>
			<span class="text-[15px] font-semibold tracking-tight">Stratum</span>
		</a>
		<!--
		
		<div class="m-2 flex h-10 items-center gap-2 rounded-lg border-1 border-black px-3">
			
			<div class="relative flex h-5 w-5 items-center justify-center">
				
				<div class="absolute top-0 left-0 h-4 w-4 rounded-full border-2 border-black"></div>
				
				<div
					class="absolute right-0 bottom-0 h-0.5 w-2 origin-bottom-right rotate-45 transform bg-black"
				></div>
			</div>

			
			<form onsubmit={searchWorkspaces}>
				<input
					bind:value={input}
					type="text"
					placeholder="Search..."
					class="w-full bg-transparent text-sm outline-none"
				/>
			</form>
		</div>
	-->
		<div class="flex items-center gap-1">
			{#each links as link}
				<a
					href={link.href}
					class="rounded-full px-4 py-2 font-mono text-xs tracking-wider uppercase transition {active ===
					link.key
						? 'bg-white/[0.06] text-white'
						: 'text-white/50 hover:text-white/80'}"
				>
					{link.label}
				</a>
			{/each}
			<button
				onclick={logout}
				class="ml-2 rounded-full border border-white/10 bg-white/[0.03] px-4 py-2 font-mono text-xs tracking-wider text-white/50 uppercase transition hover:border-[#ff3366]/30 hover:text-[#ff8fa8]"
			>
				Log out
			</button>
		</div>
	</div>
</nav>
