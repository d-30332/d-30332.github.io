<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Отчет по производственной практике — конструктор</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: #eef2f7;
            padding: 25px 15px;
            display: flex;
            justify-content: center;
        }

        .app {
            max-width: 1100px;
            width: 100%;
            background: white;
            border-radius: 28px;
            box-shadow: 0 25px 60px rgba(0,20,50,0.18);
            padding: 30px;
        }

        h1 {
            font-size: 28px;
            color: #0a2647;
            border-left: 6px solid #2a7de1;
            padding-left: 18px;
            margin-bottom: 8px;
        }

        .sub {
            color: #3d5e7a;
            margin-bottom: 30px;
            padding-left: 24px;
            font-weight: 400;
        }

        /* ===== Разделы ===== */
        .section {
            background: #f9fbfe;
            border-radius: 18px;
            padding: 20px 22px;
            margin-bottom: 25px;
            border: 1px solid #e3eaf2;
            transition: 0.2s;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            user-select: none;
        }

        .section-header h2 {
            font-size: 20px;
            color: #0b2b4a;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .section-header h2 .badge {
            font-size: 13px;
            background: #2a7de1;
            color: white;
            padding: 2px 12px;
            border-radius: 30px;
            font-weight: 500;
        }

        .section-content {
            margin-top: 18px;
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .entry-card {
            background: white;
            border-radius: 14px;
            padding: 16px 18px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
            border-left: 4px solid #2a7de1;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
        }

        .entry-card .info {
            flex: 2 1 300px;
        }

        .entry-card .info .title {
            font-weight: 600;
            color: #0a2647;
            font-size: 16px;
        }

        .entry-card .info .desc {
            color: #3e5a77;
            font-size: 14px;
            margin-top: 4px;
            white-space: pre-wrap;
        }

        .entry-card .meta {
            display: flex;
            gap: 12px;
            align-items: center;
            flex-wrap: wrap;
            margin-top: 8px;
        }

        .tag {
            background: #eaf0fa;
            padding: 2px 14px;
            border-radius: 30px;
            font-size: 12px;
            font-weight: 500;
            color: #1a4a7a;
        }

        .tag.green { background: #ddf0e4; color: #0b5531; }
        .tag.orange { background: #fff1d6; color: #8a5a00; }
        .tag.purple { background: #ede0fa; color: #5a2d8a; }

        .actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 8px 18px;
            border: none;
            border-radius: 30px;
            font-weight: 600;
            font-size: 13px;
            cursor: pointer;
            background: #e6edf6;
            color: #1f3b57;
            transition: 0.2s;
        }

        .btn-primary { background: #1a5fb4; color: white; }
        .btn-primary:hover { background: #0d4a91; }

        .btn-success { background: #1e9b5a; color: white; }
        .btn-success:hover { background: #147a46; }

        .btn-danger { background: #d9534f; color: white; }
        .btn-danger:hover { background: #b33c38; }

        .btn-outline { background: transparent; border: 2px solid #c8d8eb; }

        /* ===== Форма добавления ===== */
        .add-form {
            background: #f2f6fd;
            border-radius: 16px;
            padding: 18px 20px;
            margin-top: 8px;
            display: none;
            flex-wrap: wrap;
            gap: 12px;
            align-items: end;
            border: 2px dashed #b7cee8;
        }

        .add-form.open { display: flex; }

        .add-form .field {
            flex: 1 1 180px;
            min-width: 140px;
        }

        .add-form .field label {
            display: block;
            font-size: 12px;
            font-weight: 600;
            color: #1f4468;
            margin-bottom: 4px;
        }

        .add-form .field input,
        .add-form .field textarea,
        .add-form .field select {
            width: 100%;
            padding: 9px 12px;
            border-radius: 12px;
            border: 1px solid #cbdae9;
            font-size: 14px;
            background: white;
        }

        .add-form .field textarea {
            resize: vertical;
            min-height: 50px;
        }

        .add-form .btn {
            margin-top: 4px;
        }

        /* ===== Кнопки управления разделами ===== */
        .section-actions {
            display: flex;
            gap: 8px;
        }

        /* ===== Пустое состояние ===== */
        .empty {
            color: #7a8fa8;
            text-align: center;
            padding: 25px 10px;
            font-style: italic;
        }

        /* ===== Статистика ===== */
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
            gap: 12px;
            background: #eaf1fa;
            padding: 16px 20px;
            border-radius: 16px;
            margin-bottom: 25px;
        }

        .stats .item {
            background: white;
            padding: 10px 14px;
            border-radius: 12px;
            text-align: center;
            font-weight: 500;
            color: #1f3b57;
        }

        .stats .item span {
            display: block;
            font-size: 22px;
            font-weight: 700;
            color: #0a2647;
        }

        /* ===== Адаптив ===== */
        @media (max-width: 700px) {
            .app { padding: 16px; }
            .entry-card { flex-direction: column; align-items: stretch; }
            .section-actions { flex-wrap: wrap; }
            .add-form { flex-direction: column; }
            .add-form .field { flex: 1 1 100%; }
        }
    </style>
</head>
<body>
<div class="app" id="app">

    <h1>📋 Отчет по производственной практике</h1>
    <div class="sub">Структурированное ведение: рабочие документы · аналитика · результаты · наглядные материалы</div>

    <!-- Статистика -->
    <div class="stats">
        <div class="item">📄 Всего записей <span>{{ totalEntries }}</span></div>
        <div class="item">📊 Разделов заполнено <span>{{ filledSections }}</span>/4</div>
        <div class="item">📅 Последнее обновление <span>{{ lastUpdate }}</span></div>
    </div>

    <!-- ============================================================ -->
    <!-- РАЗДЕЛ 1: РАБОЧИЕ ДОКУМЕНТЫ -->
    <!-- ============================================================ -->
    <div class="section">
        <div class="section-header" @click="toggleSection('documents')">
            <h2>📁 1. Рабочие документы <span class="badge">{{ docs.length }}</span></h2>
            <div class="section-actions" @click.stop>
                <button class="btn btn-success" @click="openForm('documents')">+ Добавить</button>
            </div>
        </div>
        <div class="section-content">
            <div v-if="docs.length === 0" class="empty">Нет документов. Добавьте первичные учетные документы, с которыми работали.</div>
            <div v-for="(item, idx) in docs" :key="'doc'+idx" class="entry-card">
                <div class="info">
                    <div class="title">{{ item.name }}</div>
                    <div class="desc">{{ item.desc }}</div>
                    <div class="meta">
                        <span class="tag">{{ item.type || 'Документ' }}</span>
                        <span class="tag green" v-if="item.quantity">Кол-во: {{ item.quantity }}</span>
                    </div>
                </div>
                <div class="actions">
                    <button class="btn btn-outline" @click="editEntry('documents', idx)">✏️</button>
                    <button class="btn btn-danger" @click="deleteEntry('documents', idx)">🗑️</button>
                </div>
            </div>
        </div>
        <!-- Форма добавления для раздела -->
        <div class="add-form" :class="{ open: activeForm === 'documents' }">
            <div class="field"><label>Название документа</label><input v-model="docForm.name" placeholder="например: Накладная ТОРГ-12"></div>
            <div class="field"><label>Описание / что делали</label><textarea v-model="docForm.desc" placeholder="обработка, проверка, регистрация..."></textarea></div>
            <div class="field"><label>Тип</label><input v-model="docForm.type" placeholder="первичный / сводный / отчет"></div>
            <div class="field"><label>Количество</label><input v-model="docForm.quantity" placeholder="шт."></div>
            <button class="btn btn-success" @click="saveEntry('documents')">💾 Сохранить</button>
            <button class="btn btn-outline" @click="closeForm">Отмена</button>
        </div>
    </div>

    <!-- ============================================================ -->
    <!-- РАЗДЕЛ 2: АНАЛИТИКА И РАСЧЕТЫ -->
    <!-- ============================================================ -->
    <div class="section">
        <div class="section-header" @click="toggleSection('analytics')">
            <h2>📊 2. Аналитика и расчеты <span class="badge">{{ analytics.length }}</span></h2>
            <div class="section-actions" @click.stop>
                <button class="btn btn-success" @click="openForm('analytics')">+ Добавить</button>
            </div>
        </div>
        <div class="section-content">
            <div v-if="analytics.length === 0" class="empty">Нет аналитических расчетов. Добавьте расчеты показателей, оборотки, сверки.</div>
            <div v-for="(item, idx) in analytics" :key="'an'+idx" class="entry-card" style="border-left-color:#e67e22;">
                <div class="info">
                    <div class="title">{{ item.name }}</div>
                    <div class="desc">{{ item.desc }}</div>
                    <div class="meta">
                        <span class="tag orange">{{ item.method || 'Метод' }}</span>
                        <span class="tag purple" v-if="item.result">Результат: {{ item.result }}</span>
                    </div>
                </div>
                <div class="actions">
                    <button class="btn btn-outline" @click="editEntry('analytics', idx)">✏️</button>
                    <button class="btn btn-danger" @click="deleteEntry('analytics', idx)">🗑️</button>
                </div>
            </div>
        </div>
        <div class="add-form" :class="{ open: activeForm === 'analytics' }">
            <div class="field"><label>Название расчета</label><input v-model="anForm.name" placeholder="например: Оборотка по 60 счету"></div>
            <div class="field"><label>Описание / что анализировали</label><textarea v-model="anForm.desc" placeholder="анализ дебиторской задолженности..."></textarea></div>
            <div class="field"><label>Метод / формула</label><input v-model="anForm.method" placeholder="сравнение, тренд, коэффициент"></div>
            <div class="field"><label>Итоговый результат</label><input v-model="anForm.result" placeholder="сумма, % отклонения"></div>
            <button class="btn btn-success" @click="saveEntry('analytics')">💾 Сохранить</button>
            <button class="btn btn-outline" @click="closeForm">Отмена</button>
        </div>
    </div>

    <!-- ============================================================ -->
    <!-- РАЗДЕЛ 3: РЕЗУЛЬТАТЫ РАБОТЫ -->
    <!-- ============================================================ -->
    <div class="section">
        <div class="section-header" @click="toggleSection('results')">
            <h2>🏆 3. Результаты вашей работы <span class="badge">{{ results.length }}</span></h2>
            <div class="section-actions" @click.stop>
                <button class="btn btn-success" @click="openForm('results')">+ Добавить</button>
            </div>
        </div>
        <div class="section-content">
            <div v-if="results.length === 0" class="empty">Опишите, чего достигли: сформировали отчеты, закрыли периоды, выявили ошибки.</div>
            <div v-for="(item, idx) in results" :key="'res'+idx" class="entry-card" style="border-left-color:#27ae60;">
                <div class="info">
                    <div class="title">{{ item.name }}</div>
                    <div class="desc">{{ item.desc }}</div>
                    <div class="meta">
                        <span class="tag green" v-if="item.date">Дата: {{ item.date }}</span>
                        <span class="tag" v-if="item.score">Оценка: {{ item.score }}</span>
                    </div>
                </div>
                <div class="actions">
                    <button class="btn btn-outline" @click="editEntry('results', idx)">✏️</button>
                    <button class="btn btn-danger" @click="deleteEntry('results', idx)">🗑️</button>
                </div>
            </div>
        </div>
        <div class="add-form" :class="{ open: activeForm === 'results' }">
            <div class="field"><label>Название результата</label><input v-model="resForm.name" placeholder="например: Сформирована отчетность"></div>
            <div class="field"><label>Описание / что сделано</label><textarea v-model="resForm.desc" placeholder="составлен баланс, сдана декларация..."></textarea></div>
            <div class="field"><label>Дата выполнения</label><input v-model="resForm.date" type="date"></div>
            <div class="field"><label>Оценка / балл</label><input v-model="resForm.score" placeholder="5 / отлично"></div>
            <button class="btn btn-success" @click="saveEntry('results')">💾 Сохранить</button>
            <button class="btn btn-outline" @click="closeForm">Отмена</button>
        </div>
    </div>

    <!-- ============================================================ -->
    <!-- РАЗДЕЛ 4: НАГЛЯДНЫЕ МАТЕРИАЛЫ -->
    <!-- ============================================================ -->
    <div class="section">
        <div class="section-header" @click="toggleSection('visuals')">
            <h2>🖼️ 4. Наглядные материалы <span class="badge">{{ visuals.length }}</span></h2>
            <div class="section-actions" @click.stop>
                <button class="btn btn-success" @click="openForm('visuals')">+ Добавить</button>
            </div>
        </div>
        <div class="section-content">
            <div v-if="visuals.length === 0" class="empty">Добавьте ссылки на таблицы, графики, скриншоты, презентации.</div>
            <div v-for="(item, idx) in visuals" :key="'vis'+idx" class="entry-card" style="border-left-color:#8e44ad;">
                <div class="info">
                    <div class="title">{{ item.name }}</div>
                    <div class="desc">{{ item.desc }}</div>
                    <div class="meta">
                        <span class="tag purple">{{ item.type || 'Изображение' }}</span>
                        <span class="tag" v-if="item.link"><a :href="item.link" target="_blank" style="color:#1a5fb4;">🔗 Открыть</a></span>
                    </div>
                </div>
                <div class="actions">
                    <button class="btn btn-outline" @click="editEntry('visuals', idx)">✏️</button>
                    <button class="btn btn-danger" @click="deleteEntry('visuals', idx)">🗑️</button>
                </div>
            </div>
        </div>
        <div class="add-form" :class="{ open: activeForm === 'visuals' }">
            <div class="field"><label>Название материала</label><input v-model="visForm.name" placeholder="например: График динамики"></div>
            <div class="field"><label>Описание</label><textarea v-model="visForm.desc" placeholder="что изображено, какие данные"></textarea></div>
            <div class="field"><label>Тип</label><input v-model="visForm.type" placeholder="таблица / график / скриншот"></div>
            <div class="field"><label>Ссылка (или путь к файлу)</label><input v-model="visForm.link" placeholder="https://... или file://..."></div>
            <button class="btn btn-success" @click="saveEntry('visuals')">💾 Сохранить</button>
            <button class="btn btn-outline" @click="closeForm">Отмена</button>
        </div>
    </div>

    <!-- Кнопки управления данными -->
    <div style="display: flex; gap: 12px; flex-wrap: wrap; margin-top: 20px; padding-top: 18px; border-top: 2px solid #e3eaf2;">
        <button class="btn btn-primary" @click="exportData">📥 Экспорт отчета (JSON)</button>
        <button class="btn btn-outline" @click="importData">📤 Импорт (JSON)</button>
        <input type="file" id="fileInput" accept=".json" style="display:none" @change="handleImport">
        <button class="btn btn-danger" @click="clearAll">🗑️ Очистить все</button>
        <button class="btn btn-success" @click="addExamples">📌 Добавить примеры</button>
    </div>

</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.min.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            // Основные данные по разделам
            docs: [],
            analytics: [],
            results: [],
            visuals: [],
            // Формы
            activeForm: null, // 'documents', 'analytics', 'results', 'visuals'
            editIdx: null,
            // Форма для документов
            docForm: { name: '', desc: '', type: '', quantity: '' },
            anForm: { name: '', desc: '', method: '', result: '' },
            resForm: { name: '', desc: '', date: '', score: '' },
            visForm: { name: '', desc: '', type: '', link: '' },
            // Для статистики
            lastUpdate: '—'
        },
        computed: {
            totalEntries() {
                return this.docs.length + this.analytics.length + this.results.length + this.visuals.length;
            },
            filledSections() {
                let count = 0;
                if (this.docs.length > 0) count++;
                if (this.analytics.length > 0) count++;
                if (this.results.length > 0) count++;
                if (this.visuals.length > 0) count++;
                return count;
            }
        },
        methods: {
            // ---- Открытие / закрытие форм ----
            openForm(section) {
                this.activeForm = section;
                this.editIdx = null;
                // Очищаем все формы
                this.docForm = { name: '', desc: '', type: '', quantity: '' };
                this.anForm = { name: '', desc: '', method: '', result: '' };
                this.resForm = { name: '', desc: '', date: '', score: '' };
                this.visForm = { name: '', desc: '', type: '', link: '' };
            },
            closeForm() {
                this.activeForm = null;
                this.editIdx = null;
            },
            toggleSection(section) {
                // просто для аккордеона - не реализовано, т.к. все открыто
            },

            // ---- Сохранение записи ----
            saveEntry(section) {
                let form, list;
                if (section === 'documents') { form = this.docForm; list = this.docs; }
                else if (section === 'analytics') { form = this.anForm; list = this.analytics; }
                else if (section === 'results') { form = this.resForm; list = this.results; }
                else if (section === 'visuals') { form = this.visForm; list = this.visuals; }

                if (!form.name || !form.desc) {
                    alert('Заполните название и описание!');
                    return;
                }

                const entry = { ...form };

                if (this.editIdx !== null && this.editIdx < list.length) {
                    list.splice(this.editIdx, 1, entry);
                    this.editIdx = null;
                } else {
                    list.push(entry);
                }

                this.closeForm();
                this.saveToLocal();
                this.updateDate();
            },

            editEntry(section, idx) {
                let list, form;
                if (section === 'documents') { list = this.docs; form = this.docForm; }
                else if (section === 'analytics') { list = this.analytics; form = this.anForm; }
                else if (section === 'results') { list = this.results; form = this.resForm; }
                else if (section === 'visuals') { list = this.visuals; form = this.visForm; }

                const item = list[idx];
                Object.keys(form).forEach(key => { form[key] = item[key] || ''; });
                this.activeForm = section;
                this.editIdx = idx;
            },

            deleteEntry(section, idx) {
                if (!confirm('Удалить запись?')) return;
                let list;
                if (section === 'documents') list = this.docs;
                else if (section === 'analytics') list = this.analytics;
                else if (section === 'results') list = this.results;
                else if (section === 'visuals') list = this.visuals;
                list.splice(idx, 1);
                this.saveToLocal();
                this.updateDate();
                if (this.editIdx === idx) this.closeForm();
            },

            // ---- Сохранение в localStorage ----
            saveToLocal() {
                const data = {
                    docs: this.docs,
                    analytics: this.analytics,
                    results: this.results,
                    visuals: this.visuals
                };
                localStorage.setItem('practice_report_data', JSON.stringify(data));
            },
            loadFromLocal() {
                const raw = localStorage.getItem('practice_report_data');
                if (raw) {
                    try {
                        const data = JSON.parse(raw);
                        this.docs = data.docs || [];
                        this.analytics = data.analytics || [];
                        this.results = data.results || [];
                        this.visuals = data.visuals || [];
                        this.updateDate();
                    } catch(e) {}
                }
            },

            updateDate() {
                this.lastUpdate = new Date().toLocaleDateString('ru-RU', { day:'2-digit', month:'short', year:'numeric', hour:'2-digit', minute:'2-digit' });
            },

            // ---- Экспорт / Импорт ----
            exportData() {
                const data = {
                    docs: this.docs,
                    analytics: this.analytics,
                    results: this.results,
                    visuals: this.visuals,
                    exportedAt: new Date().toISOString()
                };
                const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                link.download = `practice_report_${new Date().toISOString().slice(0,10)}.json`;
                link.click();
            },
            importData() {
                document.getElementById('fileInput').click();
            },
            handleImport(e) {
                const file = e.target.files[0];
                if (!file) return;
                const reader = new FileReader();
                reader.onload = (ev) => {
                    try {
                        const data = JSON.parse(ev.target.result);
                        if (data.docs && data.analytics && data.results && data.visuals) {
                            this.docs = data.docs;
                            this.analytics = data.analytics;
                            this.results = data.results;
                            this.visuals = data.visuals;
                            this.saveToLocal();
                            this.updateDate();
                            alert('Отчет успешно загружен!');
                        } else {
                            alert('Неверный формат файла');
                        }
                    } catch(err) {
                        alert('Ошибка чтения файла');
                    }
                };
                reader.readAsText(file);
                e.target.value = '';
            },

            clearAll() {
                if (!confirm('Удалить ВСЕ данные отчета?')) return;
                this.docs = [];
                this.analytics = [];
                this.results = [];
                this.visuals = [];
                this.saveToLocal();
                this.updateDate();
                this.closeForm();
            },

            // ---- Добавление примеров для наглядности ----
            addExamples() {
                this.docs.push(
                    { name: 'Приходный ордер М-4', desc: 'Обработано 35 поступлений материалов. Проверка соответствия договорам.', type: 'первичный', quantity: '35' },
                    { name: 'Акт сверки с поставщиками', desc: 'Проведена сверка с 12 контрагентами, расхождений не выявлено.', type: 'сводный', quantity: '12' }
                );
                this.analytics.push(
                    { name: 'Оборотно-сальдовая ведомость по 60 счету', desc: 'Проанализирована кредиторская задолженность на 30.06.2026', method: 'сравнительный анализ', result: 'Задолженность снижена на 8%' },
                    { name: 'Расчет амортизации ОС', desc: 'Пересчет амортизации линейным методом за 2 квартал', method: 'линейный', result: '217 500 руб.' }
                );
                this.results.push(
                    { name: 'Сформирована отчетность', desc: 'Подготовлены оборотные ведомости и баланс для сдачи в ИФНС', date: '2026-06-28', score: '5' },
                    { name: 'Автоматизация сверки', desc: 'Настроил Excel-макрос для ускорения сверки счетов-фактур', date: '2026-06-25', score: 'отлично' }
                );
                this.visuals.push(
                    { name: 'Схема документооборота', desc: 'Схема движения первичных документов в организации', type: 'схема', link: '#' },
                    { name: 'График динамики дебиторки', desc: 'Построен график изменения дебиторской задолженности по месяцам', type: 'график', link: '#' }
                );
                this.saveToLocal();
                this.updateDate();
            }
        },
        mounted() {
            this.loadFromLocal();
            if (this.totalEntries === 0) {
                // добавим пару примеров автоматически при первом запуске
                this.addExamples();
            }
        }
    });
</script>
</body>
</html>
