# Setup dan Penggunaan Simulasi Nav2 dengan Joystick
Link Youtube: 
Dokumentasi ini menjelaskan langkah-langkah untuk mengaktifkan simulasi Nav2 pada robot menggunakan joystick sebagai kontroler.

## Persyaratan

1. **ROS 2 Humble** harus sudah terpasang di sistem Anda.
2. **Joystick** yang kompatibel dengan ROS2.
3. **Robot description dan konfigurasi Nav2** yang sudah disiapkan di workspace Anda.

## Langkah-langkah

### 1. **Sumber ROS 2 Environment**

Pastikan untuk mengatur environment ROS 2 terlebih dahulu:

```bash
source /opt/ros/humble/setup.bash
```

### 2. **Instalasi Dependensi**

Instal paket yang diperlukan untuk SLAM Toolbox (untuk perencanaan peta):

```bash
sudo apt install ros-humble-slam-toolbox
```

### 3. **Build Workspace**

Bangun workspace Anda menggunakan `colcon`:

```bash
colcon build
```

Setelah selesai, pastikan untuk mengatur environment workspace:

```bash
. install/setup.bash
```

### 4. **Menjalankan Robot Description**

Jalankan file launch yang menampilkan deskripsi robot:

```bash
ros2 launch diditrobot_description display.launch.py
```

### 5. **Menerbitkan Transformasi Statis**

Publikasikan transformasi statis antara `map` dan `odom`:

```bash
ros2 run tf2_ros static_transform_publisher 0 0 0 0 0 0 map odom
```

### 6. **Menjalankan Simulasi Nav2**

Luncurkan Nav2 dengan file konfigurasi yang sesuai:

```bash
ros2 launch nav2_bringup navigation_launch.py params_file:=/home/dietrich/tubes_ws/src/diditrobot/config/nav2_params.yaml
```

Luncurkan RViz untuk visualisasi:

```bash
ros2 launch nav2_bringup rviz_launch.py
```

### 7. **Menjalankan Node Joy**

Jalankan node `joy` untuk membaca input dari joystick:

```bash
ros2 run joy joy_node
```

### 8. **Menjalankan Teleop Twist dengan Joystick**

Jalankan node `teleop_twist_joy` untuk mengendalikan robot menggunakan joystick. Pastikan Anda sudah mengonfigurasi joystick di file `joystick_config.yaml`:

```bash
ros2 run teleop_twist_joy teleop_node --ros-args --params-file /home/dietrich/tubes_ws/src/diditrobot/config/joystick_config.yaml
```

### 9. **Verifikasi Input Joystick**

Jika joystick tidak berfungsi, Anda bisa memeriksa status joystick dengan perintah berikut:

```bash
jstest /dev/input/js0
```

Pastikan joystick Anda dikenali dan berfungsi dengan baik.

## Troubleshooting

1. **Joystick Tidak Terbaca:**
   Pastikan joystick terhubung dengan benar ke komputer Anda dan perangkat `/dev/input/js0` tersedia. Gunakan `jstest` untuk memverifikasi input joystick.

2. **Robot Tidak Bergerak:**
   - Pastikan bahwa `teleop_twist_joy` mempublikasikan pesan ke topik `/cmd_vel`. Gunakan `ros2 topic echo /cmd_vel` untuk memverifikasi.
   - Periksa apakah semua node terkait navigasi, seperti `planner_server`, `controller_server`, dan `bt_navigator`, berjalan dengan benar.

3. **Kesalahan pada Konfigurasi:**
   - Pastikan file `joystick_config.yaml` sudah sesuai dengan konfigurasi joystick yang Anda gunakan.
   - Jika ada kesalahan saat menjalankan perintah, periksa log untuk informasi lebih lanjut.

### Refrensi: https://docs.nav2.org/setup_guides/index.html
