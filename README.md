### **diditrobot**

Proyek ini adalah simulasi robot dengan empat roda menggunakan ROS 2 (Humble) dan Gazebo untuk simulasi. Berikut adalah penjelasan kode dan langkah-langkah pengoperasian robot:

---

### **Struktur Kode**

1. **Perintah untuk Memulai Simulasi:**
    
    ```bash
    colcon build
    source install/setup.bash
    ros2 launch diditrobot launch_sim.launch.py
    ```
    
    - **`colcon build`**: Membangun seluruh workspace ROS 2, termasuk paket _diditrobot_.
    - **`source install/setup.bash`**: Mengaktifkan lingkungan kerja setelah _build_ selesai.
    - **`ros2 launch diditrobot launch_sim.launch.py`**: Meluncurkan simulasi robot empat roda.
2. **Kode dan Plugin yang Digunakan:**
    
    - **Plugin Digunakan**:
        - **`libgazebo_ros_diff_drive`** untuk mengontrol roda depan dan belakang.
        - Plugin ini digunakan sebagai pengganti **`libgazebo_ros_skid_steer_drive`**, karena plugin skid steer tidak berfungsi dengan baik di konfigurasi saat ini.
    - Plugin memungkinkan kontrol gerak robot melalui perintah kecepatan (_velocity commands_).

3. **Mengontrol Robot:**
    
    - Robot dapat dikontrol menggunakan paket **teleop_twist_keyboard**:
        
        ```bash
        ros2 run teleop_twist_keyboard teleop_twist_keyboard
        ```
        
    - Paket ini memungkinkan kita untuk menggerakkan robot menggunakan input keyboard dalam terminal.

---

### **Langkah Menjalankan Simulasi**

1. **Membangun dan Menyiapkan Lingkungan:**
    
    ```bash
    colcon build
    source install/setup.bash
    ```
    
2. **Meluncurkan Simulasi:**
    
    ```bash
    ros2 launch diditrobot launch_sim.launch.py
    ```
    
3. **Mengontrol Robot:**
    
    - Jalankan teleop:
        
        ```bash
        ros2 run teleop_twist_keyboard teleop_twist_keyboard
        ```
        
    - Gunakan tombol panah atau WASD untuk menggerakkan robot.
4. **Beralih Antara Resolusi Rendah dan Tinggi:**
    
    - Edit file **`robot.urdf.xacro`** dan komentari salah satu dari:
        - **`robot_core_lr.xacro`** (resolusi rendah).
        - **`robot_core_hr.xacro`** (resolusi tinggi).

---

### **Refrensi**

Proyek ini terinspirasi dan menggunakan referensi dari repositori berikut:

- **Repository:** [four_wheeled_robot by Micky Sukmana](https://github.com/MickySukmana/four_wheeled_robot)
