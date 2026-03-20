<script lang="ts">
	const organizers = [
		{ name: 'Jarod Alper', department: 'Mathematics', role: 'Faculty', website: '' },
		{ name: 'Vasily Ilin', department: 'Mathematics', role: 'Faculty', website: '' },
		{ name: 'Dhruv Bhatia', department: 'Mathematics', role: 'Organizer', website: '' },
		{ name: 'Michael Zeng', department: 'Mathematics', role: 'Organizer', website: 'https://zengrf.github.io' },
		{ name: 'Oliver Flatt', department: 'PLSE', role: 'Organizer', website: '' },
		{ name: 'Zachary Tatlock', department: 'PLSE', role: 'Faculty', website: '' },
		{ name: 'Gilbert Bernstein', department: 'PLSE', role: 'Faculty', website: '' },
		{ name: 'Eric Klavins', department: 'ECE', role: 'Faculty', website: '' }
	];

	function getInitials(name: string): string {
		return name.split(' ').map(n => n[0]).join('');
	}

	function getDeptColor(dept: string): string {
		const colors: Record<string, string> = {
			'Mathematics': '#a87cff',
			'PLSE': '#f0cc5b',
			'ECE': '#7cf0b5'
		};
		return colors[dept] || '#8b54fa';
	}
</script>

<section id="organizers" class="section">
	<div class="container">
		<h2 class="section-title">Organizers</h2>

		<div class="organizers-grid">
			{#each organizers as person, i}
				{#if person.website}
					<a href={person.website} target="_blank" rel="noopener" class="organizer-card glass-card linkable" style="animation-delay: {i * 0.08}s">
						<div class="avatar" style="border-color: {getDeptColor(person.department)}">
							<span class="avatar-initials" style="color: {getDeptColor(person.department)}">{getInitials(person.name)}</span>
						</div>
						<h3>{person.name}</h3>
						<span class="dept" style="color: {getDeptColor(person.department)}">{person.department}</span>
						<span class="role">{person.role}</span>
					</a>
				{:else}
					<div class="organizer-card glass-card" style="animation-delay: {i * 0.08}s">
						<div class="avatar" style="border-color: {getDeptColor(person.department)}">
							<span class="avatar-initials" style="color: {getDeptColor(person.department)}">{getInitials(person.name)}</span>
						</div>
						<h3>{person.name}</h3>
						<span class="dept" style="color: {getDeptColor(person.department)}">{person.department}</span>
						<span class="role">{person.role}</span>
					</div>
				{/if}
			{/each}
		</div>
	</div>
</section>

<style>
	.organizers-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
		gap: 1.25rem;
		margin-bottom: 4rem;
	}

	.organizer-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		padding: 2rem 1.5rem;
		animation: fadeInUp 0.6s ease both;
	}

	.avatar {
		width: 70px;
		height: 70px;
		border-radius: 50%;
		border: 2px solid;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 1rem;
		background: rgba(139, 84, 250, 0.08);
	}

	.avatar-initials {
		font-size: 1.3rem;
		font-weight: 700;
		font-family: var(--font-mono);
	}

	.organizer-card h3 {
		font-size: 1rem;
		color: var(--text-heading);
		margin-bottom: 0.3rem;
	}

	.dept {
		font-size: 0.8rem;
		font-weight: 600;
	}

	.role {
		font-size: 0.75rem;
		color: var(--text-muted);
		margin-top: 0.2rem;
	}

	a.organizer-card {
		text-decoration: none;
		color: inherit;
		cursor: pointer;
	}

	.linkable:hover {
		border-color: rgba(139, 84, 250, 0.5);
		box-shadow: 0 20px 60px rgba(107, 63, 160, 0.2);
	}

	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@media (max-width: 768px) {
		.organizers-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}
</style>
