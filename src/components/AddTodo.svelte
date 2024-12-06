<script lang="ts">
	// ประกาศฟังก์ชัน onAdd ที่จะถูกเรียกเมื่อมีการเพิ่มรายการ Todo
	export let onAdd: (text: string) => void;

	let text = '';

	// ฟังก์ชันสำหรับเพิ่ม Todo และ ตรวจสอบว่าข้อความไม่เป็นค่าว่าง
	const addTodo = () => {
		if (text.trim() !== '') {
			onAdd(text);
			text = '';
		}
	};

	// ฟังก์ชันที่ใช้สำหรับการกด Enter เพื่อเพิ่ม Todo
	const handleKeydown = (event: KeyboardEvent) => {
		if (event.key === 'Enter') {
			addTodo();
		}
	};
</script>

<div class="input-container">
	<input type="text" bind:value={text} on:keydown={handleKeydown} placeholder="เพิ่มรายการใหม่" />
	<button class="add-btn" on:click={addTodo}>เพิ่ม</button>
</div>

<style>
	.input-container {
		display: flex;
		align-items: center;
		width: 100%;
		justify-content: center;
		gap: 0;
		margin-bottom: 30px;
		transition: 0.3s;
	}

	.input-container:hover {
		transform: scale(1.08);
	}

	input {
		margin: 0;
		border: none;
		width: 400px;
		height: 40px;
		padding: 0 15px;
		border-top-left-radius: 20px;
		border-bottom-left-radius: 20px;
		font-family: 'Kanit', sans-serif;
		outline: none;
		transition: 0.3s;
	}

	input:focus {
		border-color: #007bff;
	}

	.add-btn {
		border: none;
		background-color: #007bff;
		color: white;
		border-top-right-radius: 20px;
		border-bottom-right-radius: 20px;
		padding: 0;
		width: 80px;
		height: 40px;
		cursor: pointer;
		font-family: 'Kanit', sans-serif;
		font-size: 14px;
	}

	.add-btn:hover {
		background-color: #0056b3;
	}

	@media (max-width: 618px) {
		.input-container {
			width: 80%;
		}
	}
</style>
