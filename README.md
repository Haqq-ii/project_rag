3. Alur Kerja Workflow
Alur data yang berjalan pada Workflow TeleeBot adalah sebagai berikut:
User → Telegram Bot → Ngrok Tunnel → Telegram Trigger (n8n) → AI Agent → OpenAI Chat Model → Send a text message → Telegram → User
Penjelasan node per node:
1) Telegram Trigger (Updates: message)
Node ini mendeteksi pesan masuk dari Telegram Bot. Ketika pengguna mengirimkan teks apa pun, node ini menghasilkan event lalu meneruskannya ke node berikutnya.
2) AI Agent
Node AI Agent menerima pesan dari Telegram Trigger.
Fungsinya:
Mengatur alur prompt masuk dan keluar
Mengakses model OpenAI melalui input Chat Model
Menjadi "router" antara pesan user dan OpenAI
Node ini terhubung ke OpenAI Chat Model melalui port Chat Model.
3) OpenAI Chat Model
Node ini menjalankan model OpenAI (misalnya GPT-4 atau GPT-3.5).
Perannya:
Menerima prompt dari AI Agent
Menghasilkan jawaban berbasis AI
Mengembalikan hasil kembali ke AI Agent
4) Send a text message
Node ini mengirimkan hasil respons AI ke Telegram Bot. Output yang dikirim berupa teks yang sudah diproses oleh OpenAI.
4. Pengujian
Pengujian dilakukan dengan cara:
Menjalankan Ngrok untuk membuka port 5678 ke publik
 contoh: https://imperious-susie-divaricately.ngrok-free.dev
Mengatur webhook Telegram menggunakan URL Ngrok.
Mengaktifkan workflow di n8n.
Mengirimkan pesan melalui Telegram Bot.
Hasil pengujian menunjukkan bahwa:
Pesan berhasil diterima oleh node Telegram Trigger
AI Agent memproses input dengan baik
OpenAI Chat Model menghasilkan jawaban
Node Send a Text Message mengirimkan balasan ke Telegram
Percakapan berjalan dua arah tanpa error
