<script lang="ts">
	import type { Todo } from '../types';

	export let todo: Todo;
	export let onToggle: (id: number) => void;
	export let onDelete: (id: number) => void;
	export let onEdit: (id: number, newText: string) => void;

	let isEditing = false;
	let newText = todo.text;

	// ฟังก์ชันสำหรับบันทึกข้อความที่แก้ไข
	const saveEdit = () => {
		isEditing = false;
		onEdit(todo.id, newText);
	};

	// ฟังก์ชันสำหรับลบรายการ
	const deleteItem = () => {
		onDelete(todo.id);
	};

	// ฟังก์ชันสำหรับสลับสถานะ Completed/Pending
	const toggleStatus = () => {
		onToggle(todo.id);
	};
</script>

<div class="todo-item">
	<!-- Checkbox สำหรับสลับสถานะ Completed/Pending -->
	<label class="checkbox-container">
		<input type="checkbox" checked={todo.completed} on:change={toggleStatus} />
		<span class="checkmark"></span>
	</label>

	{#if isEditing}
		<!-- ช่องแก้ไขข้อความ -->
		<input
			type="text"
			bind:value={newText}
			on:blur={saveEdit}
			on:keydown={(e) => e.key === 'Enter' && saveEdit()}
		/>
	{:else}
		<!-- ข้อความ Todo สามารถคลิกเพื่อแก้ไขได้ -->
		<button
			id="todo-text"
			class={todo.completed ? 'completed' : ''}
			on:click={() => (isEditing = true)}
		>
			{todo.text}
		</button>
	{/if}

	<!-- แสดงสถานะ -->
	<span class="status">
		{#if todo.completed}
			<span class="completed-status">ทำแล้ว (Completed)</span>
		{:else}
			<span class="pending-status">ยังไม่ทำ (Pending)</span>
		{/if}
	</span>

	<!-- ปุ่มลบ -->
	<button class="delete-btn" on:click={deleteItem}>ลบ</button>
</div>

<style>
	.todo-item {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 10px;
		height: 20px;
		width: 400px;
		padding: 10px;
		border-radius: 20px;
		background-color: white;
		transition: 0.3s;
		position: relative;
		overflow: hidden;
	}

	.todo-item:hover {
		transform: scale(1.08);
	}

	.checkbox-container {
		display: flex;
		align-items: center;
		position: relative;
		cursor: pointer;
	}

	input[type='checkbox'] {
		opacity: 0; /* ซ่อน checkbox ดั้งเดิม */
		position: absolute; /* ทำให้ไม่รบกวน layout */
	}

	.checkmark {
		width: 20px;
		height: 20px;
		border: 2px solid #2d3242;
		border-radius: 50%;
		background-color: white;
		transition:
			background-color 0.3s,
			border-color 0.3s;
	}

	input[type='checkbox']:checked + .checkmark {
		background-color: #2d3242;
		border-color: #2d3242;
	}

	input[type='checkbox']:checked + .checkmark::after {
		content: '';
		position: absolute;
		left: 8px;
		top: 4px;
		width: 5px;
		height: 10px;
		border: solid white;
		border-width: 0 2px 2px 0;
		transform: rotate(45deg);
	}

	#todo-text {
		background-color: transparent;
		color: #2d3242;
		width: 160px;
	}

	.status {
		font-size: 0.7rem;
		color: gray;
		margin-right: 70px;
		cursor: default;
	}

	.completed-status {
		color: rgb(0, 255, 89);
		font-weight: bold;
	}

	.pending-status {
		color: gray;
	}

	.completed {
		text-decoration: line-through;
		color: rgb(128, 128, 128);
	}

	input[type='text'] {
		width: 150px;
		margin: 0;
		padding-left: 10px;
		border-radius: 20px;
		font-family: 'Kanit', sans-serif;
		border: 1px solid rgb(128, 128, 128);
	}

	input[type='text']:focus {
		outline-width: 0;
	}

	.delete-btn {
		position: absolute;
		right: 0;
		top: 50%;
		transform: translateY(-50%);
		color: #fff;
		background-color: red;
		height: 50px;
		width: 50px;
		border: none;
		cursor: pointer;
	}

	.delete-btn:hover {
		background-color: rgb(197, 0, 0);
		box-shadow: 1px 1px 10px rgb(255, 39, 39);
	}

	@media (max-width: 618px) {
		.todo-item {
			width: 100%;
		}

		input[type='text'] {
			font-size: 12px;
			width: 100px;
			margin: 0 15px;
		}

		#todo-text {
			font-size: 12px;
		}

		.status {
			margin-right: 50px;
			cursor: default;
			font-size: 10px;
			text-align: center;
		}
	}
</style>
