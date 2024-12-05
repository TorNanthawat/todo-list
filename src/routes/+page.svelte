<script lang="ts">
	import AddTodo from '../components/AddTodo.svelte';
	import TodoList from '../components/TodoList.svelte';
	import { onMount } from 'svelte';

	type Todo = {
		id: number;
		text: string;
		completed: boolean;
	};

	let todos: Todo[] = [];

	// ฟังก์ชันสำหรับดึงข้อมูลจาก LocalStorage เมื่อแอปโหลด / เปลี่ยนจาก string กลับเป็น array
	const loadTodos = () => {
		try {
			const storedTodos = localStorage.getItem('todos');
			if (storedTodos) {
				todos = JSON.parse(storedTodos);
			}
		} catch (error) {
			console.error('เกิดข้อผิดพลาดในการโหลด todo จาก localStorage:', error);
			todos = [];
		}
	};

	// ฟังก์ชันสำหรับบันทึกข้อมูลลง LocalStorage / แปลงเป็น string ก่อนเก็บ
	const saveTodos = () => {
		try {
			localStorage.setItem('todos', JSON.stringify(todos));
		} catch (error) {
			console.error('เกิดข้อผิดพลาดในการบันทึก todo ไปยัง localStorage:', error);
		}
	};

	// ฟังก์ชัน onMount ให้ทำงานเฉพาะใน Client-Side
	onMount(() => {
		loadTodos(); // เรียกใช้ฟังก์ชัน loadTodos หลังจากหน้าเว็บโหลดแล้ว
	});

	// ฟังก์ชันสำหรับเพิ่ม Todo
	const addTodo = (text: string) => {
		const newTodo: Todo = { id: Date.now(), text, completed: false };
		todos = [...todos, newTodo];
		saveTodos();
	};

	// ฟังก์ชันสำหรับเปลี่ยนสถานะ Completed/Pending
	const toggleTodo = (id: number) => {
		todos = todos.map((todo) => (todo.id === id ? { ...todo, completed: !todo.completed } : todo));
		saveTodos();
	};

	// ฟังก์ชันสำหรับลบ Todo
	const deleteTodo = (id: number) => {
		todos = todos.filter((todo) => todo.id !== id);
		saveTodos();
	};

	// ฟังก์ชันสำหรับแก้ไขข้อความของ Todo
	const editTodo = (id: number, newText: string) => {
		todos = todos.map((todo) => (todo.id === id ? { ...todo, text: newText } : todo));
		saveTodos();
	};
</script>

<div class="todo-app">
	<AddTodo onAdd={addTodo} />
	<TodoList {todos} onToggle={toggleTodo} onDelete={deleteTodo} onEdit={editTodo} />
</div>

<style>
	.todo-app {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
	}
</style>
