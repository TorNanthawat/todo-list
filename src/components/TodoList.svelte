<script lang="ts">
	import TodoItem from './TodoItem.svelte';
	import type { Todo } from '../types';

	export let todos: Todo[] = [];
	// ประกาศฟังก์ชันสำหรับจัดการการเปลี่ยนแปลงสถานะ, การลบ, และการแก้ไข
	export let onToggle: (id: number) => void;
	export let onDelete: (id: number) => void;
	export let onEdit: (id: number, newText: string) => void;
</script>

<div>
	<!-- ตรวจสอบว่ามีรายการ Todo หรือไม่ ให้แสดงข้อความถ้าไม่มี Todo -->
	{#if todos.length > 0}
		{#each todos as todo (todo.id)}
			<TodoItem {todo} {onToggle} {onDelete} {onEdit} />
		{/each}
	{:else}
		<p>ยังไม่มีรายการ Todo</p>
	{/if}
</div>

<style>
	p {
		text-align: center;
	}

	div {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		gap: 0;
		margin-bottom: 30px;
		transition: 0.3s;
	}

	@media (max-width: 618px) {
		div {
			width: 65%;
		}
	}
</style>
