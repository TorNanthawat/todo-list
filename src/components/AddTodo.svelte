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
</script>

<div>
	<input type="text" bind:value={text} placeholder="เพิ่มรายการใหม่" />
	<button class="add-btn" on:click={addTodo}>เพิ่ม</button>
</div>

<style>
	div {
		display: flex;
		gap: 0;
		margin-bottom: 30px;
		transition: 0.3s;
	}
	div:hover {
		transform: scale(1.08);
	}

	input {
		margin: 0;
		border: 0;
		width: 300px;
		height: 40px;
		padding-left: 15px;
		border-top-left-radius: 20px;
		border-bottom-left-radius: 20px;
		font-family: 'Kanit', sans-serif;
		outline-width: 0;
		transition: 0.3s;
	}

	input:focus {
		outline-width: 0;
	}

	.add-btn {
		border-top-right-radius: 20px;
		border-bottom-right-radius: 20px;
		width: 80px;
		height: 42px;
		padding: 10px 10px 10px 0;
	}
</style>
