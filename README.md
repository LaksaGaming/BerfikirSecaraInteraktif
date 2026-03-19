<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luxury Tasks · reminder dashboard</title>
    <!-- google fonts & font awesome for that premium feel -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 10% 30%, #1e1a2f, #0c0b14);
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1.5rem;
        }

        /* glassmorphic card container — mewah & modern */
        .dashboard {
            max-width: 1000px;
            width: 100%;
            background: rgba(20, 18, 32, 0.65);
            backdrop-filter: blur(14px) saturate(180%);
            -webkit-backdrop-filter: blur(14px) saturate(180%);
            border: 1px solid rgba(230, 220, 255, 0.15);
            border-radius: 3rem;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(200, 180, 255, 0.1) inset, 0 0 30px rgba(150, 100, 255, 0.2);
            padding: 2.5rem 2.2rem;
            transition: all 0.3s ease;
        }

        /* header section with subtle gold accent */
        .header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 2rem;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .title-section h1 {
            font-weight: 600;
            font-size: 2.2rem;
            letter-spacing: -0.02em;
            background: linear-gradient(135deg, #f0eaff, #cfc1ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 0.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .title-section h1 i {
            font-size: 2rem;
            color: #c9b6ff;
            text-shadow: 0 0 15px #a67cff;
        }

        .subhead {
            font-weight: 300;
            font-size: 0.95rem;
            color: #a99ed6;
            letter-spacing: 0.3px;
            border-left: 2px solid rgba(200, 180, 255, 0.5);
            padding-left: 0.8rem;
        }

        .date-badge {
            background: rgba(45, 35, 65, 0.7);
            border: 1px solid rgba(255, 215, 200, 0.15);
            border-radius: 60px;
            padding: 0.65rem 1.8rem;
            backdrop-filter: blur(4px);
            box-shadow: 0 8px 16px -8px black;
        }

        .date-badge i {
            color: #d9c9ff;
            margin-right: 10px;
            font-size: 1.1rem;
        }

        .date-badge span {
            font-weight: 500;
            color: #f2eaff;
            font-size: 1rem;
        }

        /* add task area — elegan */
        .add-task {
            background: rgba(12, 10, 22, 0.7);
            border-radius: 3rem;
            padding: 0.6rem 0.6rem 0.6rem 1.8rem;
            margin: 2rem 0 2.5rem 0;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            border: 1px solid rgba(210, 190, 255, 0.2);
            box-shadow: 0 20px 30px -20px #000000cc, 0 0 0 1px rgba(240, 230, 255, 0.05) inset;
            backdrop-filter: blur(10px);
        }

        .add-task i {
            color: #b4a0ff;
            font-size: 1.3rem;
        }

        .add-task input {
            flex: 1;
            background: transparent;
            border: none;
            padding: 1rem 0.5rem;
            font-size: 1.1rem;
            font-weight: 400;
            color: #f0eaff;
            outline: none;
        }

        .add-task input::placeholder {
            color: #6a5f8a;
            font-weight: 300;
            letter-spacing: -0.2px;
        }

        .add-task button {
            background: linear-gradient(145deg, #2b2344, #18142b);
            border: none;
            border-radius: 3rem;
            padding: 0.9rem 2.2rem;
            color: #f3ebff;
            font-weight: 600;
            font-size: 1rem;
            letter-spacing: 0.3px;
            cursor: pointer;
            box-shadow: 0 6px 14px rgba(0, 0, 0, 0.7), 0 0 0 1px #7364b9 inset, 0 0 15px #5f4b9b;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            gap: 10px;
            backdrop-filter: blur(5px);
        }

        .add-task button i {
            color: #cfbdff;
            font-size: 1.1rem;
        }

        .add-task button:hover {
            background: linear-gradient(145deg, #332b52, #201d38);
            box-shadow: 0 8px 18px #000000, 0 0 0 2px #9d86e6 inset, 0 0 30px #784fff;
            transform: scale(1.02);
            color: white;
        }

        /* task counter + elegant filter */
        .stats {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1.5rem;
            padding: 0 0.4rem;
        }

        .counter {
            color: #b6a7e6;
            font-weight: 300;
            background: rgba(25, 20, 40, 0.5);
            padding: 0.4rem 1.2rem;
            border-radius: 40px;
            border: 1px solid rgba(255, 255, 255, 0.06);
            font-size: 0.95rem;
        }

        .counter strong {
            color: #e7daff;
            font-weight: 600;
            font-size: 1.2rem;
            margin-right: 5px;
        }

        .filter-badge {
            display: flex;
            gap: 0.8rem;
            color: #9c8cc2;
        }

        .filter-badge span {
            cursor: pointer;
            padding: 0.3rem 0.8rem;
            border-radius: 30px;
            transition: 0.2s;
            font-weight: 400;
            background: rgba(30, 24, 48, 0.4);
            border: 1px solid transparent;
        }

        .filter-badge span.active {
            background: rgba(128, 96, 255, 0.2);
            border: 1px solid #a07dff;
            color: #f3e9ff;
            font-weight: 500;
            box-shadow: 0 0 15px #632efb3b;
        }

        .filter-badge span i {
            margin-right: 6px;
            font-size: 0.8rem;
            color: #b29eff;
        }

        /* task list — mewah, setiap item seperti permata */
        .task-list {
            display: flex;
            flex-direction: column;
            gap: 0.9rem;
            max-height: 380px;
            overflow-y: auto;
            padding-right: 0.4rem;
            margin-top: 0.8rem;
        }

        /* custom scrollbar — luxury touch */
        .task-list::-webkit-scrollbar {
            width: 6px;
        }

        .task-list::-webkit-scrollbar-track {
            background: rgba(30, 25, 45, 0.7);
            border-radius: 20px;
        }

        .task-list::-webkit-scrollbar-thumb {
            background: rgba(170, 140, 250, 0.4);
            border-radius: 20px;
            border: 1px solid rgba(200, 170, 255, 0.2);
        }

        .task-item {
            background: rgba(18, 15, 32, 0.7);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(230, 210, 255, 0.1);
            border-radius: 3rem;
            padding: 0.9rem 1.7rem 0.9rem 2rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 18px 28px -18px #000000, 0 0 0 1px rgba(220, 200, 255, 0.08) inset;
            transition: all 0.2s ease;
        }

        .task-item:hover {
            border-color: rgba(190, 160, 255, 0.3);
            box-shadow: 0 20px 30px -18px #26004e, 0 0 0 1px #b192ff3b inset;
            background: rgba(24, 19, 40, 0.8);
            transform: translateY(-2px);
        }

        .task-info {
            display: flex;
            align-items: center;
            gap: 1.2rem;
            flex: 1;
        }

        .task-check {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            border: 2px solid rgba(210, 190, 255, 0.5);
            background: transparent;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: transparent;
            font-size: 0.8rem;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 0 10px #5940a0;
        }

        .task-item.completed .task-check {
            background: radial-gradient(circle at 30% 30%, #bc9eff, #8b6de0);
            border-color: #bba4ff;
            color: #0c081c;
            box-shadow: 0 0 20px #bf9fff;
        }

        .task-item.completed .task-check i {
            color: #0f0b1f;
            font-size: 0.7rem;
        }

        .task-text {
            font-size: 1.2rem;
            font-weight: 450;
            color: #f2e9ff;
            letter-spacing: -0.2px;
            transition: 0.2s;
        }

        .task-item.completed .task-text {
            text-decoration: line-through;
            text-decoration-color: #aa9ace;
            color: #9b8bbc;
            font-weight: 350;
        }

        .task-actions {
            display: flex;
            gap: 0.9rem;
            align-items: center;
        }

        .task-actions i {
            font-size: 1.2rem;
            color: #8d7fb0;
            cursor: pointer;
            transition: 0.2s;
            padding: 6px;
            border-radius: 50%;
        }

        .task-actions i.fa-pen:hover {
            color: #dac3ff;
            text-shadow: 0 0 15px #caadff;
            background: rgba(255, 255, 255, 0.02);
        }

        .task-actions i.fa-trash:hover {
            color: #ffb0b0;
            text-shadow: 0 0 15px #ff8080;
            background: rgba(180, 100, 100, 0.1);
        }

        .empty-message {
            text-align: center;
            padding: 3rem 2rem;
            color: #6b5e8c;
            font-style: italic;
            border: 1px dashed rgba(170, 150, 240, 0.3);
            border-radius: 4rem;
            background: rgba(10, 8, 22, 0.4);
            backdrop-filter: blur(6px);
        }

        .empty-message i {
            font-size: 3rem;
            opacity: 0.5;
            margin-bottom: 0.8rem;
        }

        footer {
            margin-top: 2rem;
            font-size: 0.8rem;
            text-align: right;
            color: #5d4f82;
            border-top: 0.5px solid rgba(255, 255, 255, 0.04);
            padding-top: 1.2rem;
        }

        footer i {
            color: #b197fc;
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <!-- header mewah -->
        <div class="header">
            <div class="title-section">
                <h1>
                    <i class="fas fa-gem"></i> kerjaan.remind
                </h1>
                <div class="subhead">elevated task manager / karya mewah</div>
            </div>
            <div class="date-badge">
                <i class="fas fa-calendar-alt"></i>
                <span id="currentDate"></span>
            </div>
        </div>

        <!-- input tambah kerjaan (glossy) -->
        <div class="add-task">
            <i class="fas fa-plus-circle"></i>
            <input type="text" id="taskInput" placeholder="tambah kerjaan baru ... (contoh: revisi klien)" autocomplete="off">
            <button id="addTaskBtn">
                <i class="fas fa-feather-alt"></i> tambah
            </button>
        </div>

        <!-- statistik dan filter sederhana -->
        <div class="stats">
            <div class="counter" id="taskCounter">
                <strong id="countValue">0</strong> kerjaan
            </div>
            <div class="filter-badge">
                <span class="active" data-filter="all"><i class="fas fa-list-ul"></i> semua</span>
                <span data-filter="active"><i class="fas fa-spinner"></i> aktif</span>
                <span data-filter="completed"><i class="fas fa-check-circle"></i> selesai</span>
            </div>
        </div>

        <!-- Daftar tugas yang akan diisi javascript -->
        <div class="task-list" id="taskListContainer">
            <!-- akan diisi secara dinamis, jika kosong muncul empty state -->
            <div class="empty-message" id="emptyState">
                <i class="fas fa-cloud-moon"></i>
                <p>belum ada kerjaan, santai dulu ... atau tambah yang baru</p>
            </div>
        </div>

        <!-- footer estetik -->
        <footer>
            <i class="fas fa-crown"></i> luxury dashboard • kerjaan & pengingat
        </footer>
    </div>

    <script>
        (function(){
            // state data — simpan di memory, bisa dikembangkan localstorage
            let tasks = [
                { id: '1', text: 'Finalisasi proposal klien A', completed: false },
                { id: '2', text: 'Meeting tim kreatif 14.00', completed: false },
                { id: '3', text: 'Review draft konten', completed: true },
                { id: '4', text: 'Kirim invoice ke finance', completed: false }
            ];

            // variable filter aktif (all / active / completed)
            let currentFilter = 'all';

            // elemen dom
            const taskListEl = document.getElementById('taskListContainer');
            const emptyStateEl = document.getElementById('emptyState');
            const addBtn = document.getElementById('addTaskBtn');
            const taskInput = document.getElementById('taskInput');
            const countSpan = document.getElementById('countValue');
            const filterSpans = document.querySelectorAll('.filter-badge span');

            // helper: generate id simpel
            function generateId() {
                return Date.now() + '-' + Math.random().toString(36).substr(2, 9);
            }

            // render task berdasarkan filter
            function renderTasks() {
                // saring task
                let filteredTasks = tasks;
                if (currentFilter === 'active') {
                    filteredTasks = tasks.filter(t => !t.completed);
                } else if (currentFilter === 'completed') {
                    filteredTasks = tasks.filter(t => t.completed);
                }

                // update counter total (selalu dari tasks length, bukan filtered)
                const activeCount = tasks.filter(t => !t.completed).length;
                const totalCount = tasks.length;
                countSpan.innerText = totalCount;

                // kalau filteredTasks kosong tampilkan empty state
                if (filteredTasks.length === 0) {
                    let emptyMsg = '';
                    if (currentFilter === 'all') emptyMsg = 'belum ada kerjaan, tambah yuk ✨';
                    else if (currentFilter === 'active') emptyMsg = 'tidak ada kerjaan aktif · semua sudah selesai?';
                    else emptyMsg = 'belum ada kerjaan yang selesai · semangat!';
                    taskListEl.innerHTML = `<div class="empty-message"><i class="fas fa-cloud-moon"></i><p>${emptyMsg}</p></div>`;
                    return;
                }

                // bangun html task
                let htmlString = '';
                filteredTasks.forEach(task => {
                    const completedClass = task.completed ? 'completed' : '';
                    const checkIcon = task.completed ? '<i class="fas fa-check"></i>' : '';
                    
                    htmlString += `
                        <div class="task-item ${completedClass}" data-task-id="${task.id}">
                            <div class="task-info">
                                <span class="task-check" data-check="toggle">${checkIcon}</span>
                                <span class="task-text">${escapeHtml(task.text)}</span>
                            </div>
                            <div class="task-actions">
                                <i class="fas fa-pen" data-action="edit"></i>
                                <i class="fas fa-trash" data-action="delete"></i>
                            </div>
                        </div>
                    `;
                });

                taskListEl.innerHTML = htmlString;
            }

            // simple escape
            function escapeHtml(unsafe) {
                return unsafe.replace(/[&<>"]/g, function(m) {
                    if (m === '&') return '&amp;';
                    if (m === '<') return '&lt;';
                    if (m === '>') return '&gt;';
                    if (m === '"') return '&quot;';
                    return m;
                });
            }

            // toggle completed
            function toggleTask(taskId) {
                const task = tasks.find(t => t.id === taskId);
                if (task) {
                    task.completed = !task.completed;
                    renderTasks();
                }
            }

            // edit task dengan prompt (bisa pakai modal, tapi simple biar mewah prompt)
            function editTask(taskId) {
                const task = tasks.find(t => t.id === taskId);
                if (!task) return;
                const newText = prompt('Edit kerjaan:', task.text);
                if (newText !== null && newText.trim() !== '') {
                    task.text = newText.trim();
                    renderTasks();
                } else if (newText !== null && newText.trim() === '') {
                    alert('kerjaan tidak boleh kosong');
                }
            }

            // delete task
            function deleteTask(taskId) {
                tasks = tasks.filter(t => t.id !== taskId);
                renderTasks();
            }

            // tambah task baru
            function addNewTask() {
                const text = taskInput.value.trim();
                if (text === '') {
                    alert('tulis kerjaan dulu ...');
                    return;
                }
                const newTask = {
                    id: generateId(),
                    text: text,
                    completed: false
                };
                tasks.push(newTask);
                taskInput.value = '';  // kosongkan input
                // jika filter sedang completed, kadang user mau lihat langsung. Pindah ke all biar keliatan
                // biar nyaman, kita pindah filter ke 'all'
                if (currentFilter !== 'all') {
                    // ubah active filter
                    currentFilter = 'all';
                    filterSpans.forEach(s => {
                        const filterVal = s.getAttribute('data-filter');
                        if (filterVal === currentFilter) s.classList.add('active');
                        else s.classList.remove('active');
                    });
                }
                renderTasks();
            }

            // event delegation untuk taskList (toggle, edit, delete)
            taskListEl.addEventListener('click', (e) => {
                const target = e.target;
                const taskItem = target.closest('.task-item');
                if (!taskItem) return;
                const taskId = taskItem.getAttribute('data-task-id');

                // cek apakah klik di checkbox / icon didalamnya
                if (target.closest('.task-check') || target.classList.contains('task-check') || target.parentElement?.classList.contains('task-check')) {
                    toggleTask(taskId);
                }
                else if (target.closest('[data-action="edit"]')) {
                    editTask(taskId);
                }
                else if (target.closest('[data-action="delete"]')) {
                    if (confirm('Hapus kerjaan ini?')) {
                        deleteTask(taskId);
                    }
                }
            });

            // filter click
            filterSpans.forEach(span => {
                span.addEventListener('click', () => {
                    filterSpans.forEach(s => s.classList.remove('active'));
                    span.classList.add('active');
                    currentFilter = span.getAttribute('data-filter');
                    renderTasks();
                });
            });

            // tambah task via button
            addBtn.addEventListener('click', addNewTask);

            // tambah task via enter di input
            taskInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    addNewTask();
                }
            });

            // set current date (untuk mempercantik date badge)
            function setDate() {
                const now = new Date();
                const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
                const formatted = now.toLocaleDateString('id-ID', { day: 'numeric', month: 'long', year: 'numeric' });
                document.getElementById('currentDate').innerText = formatted;
            }
            setDate();

            // render awal
            renderTasks();
        })();
    </script>
</body>
</html>
