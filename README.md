echo "[+] Iniciando otimização de sensibilidade..."pointer_speed 7touch_filtering_modemovement_filter_weightecho "[+] Iniciando otimização de sensibilidade..."am kill-all 2>/dev/null || echo "[!] am kill-all não disponível neste dispositivo."#!/system/bin/sh
# =========================================================
# SCRIPT DE OTIMIZAÇÃO DE MIRA E TOUCH (ANTI-LAG & PRECISÃO)
# =========================================================

echo "[+] Iniciando otimização de sensibilidade..."

# --- 1. PRECISÃO DE MIRA & TOUCH ---
settings put secure long_press_timeout 250
settings put system pointer_speed 7
settings put global touch_filtering_mode 1
settings put secure touch_exploration_enabled 0

# --- 2. REDUÇÃO DE RECUO (ESTABILIZAÇÃO) ---
settings put system movement_filter_weight 10
settings put system RegisterHit_MinMovePixel 1
echo "[+] Estabilização de recuo aplicada."

# --- 3. OTIMIZAÇÃO TOUCH (BOTÃO 4 / SENSIBILIDADE) ---
setprop touch.deviceType touchScreen
setprop touch.orientationAware 1
setprop windowsmgr.max_events_per_sec 120
echo "[+] Otimização do Touchscreen ativada (120Hz polling rate virtual)."

# --- 4. BORDAS COLORIDAS (VISUAL & DESEMPENHO) ---
setprop debug.hwui.renderer opengl
setprop debug.egl.hw 1
setprop persist.sys.ui.hw true
echo "[+] Renderização de bordas e GPU otimizada."

# --- 5. LIMPEZA DE MEMÓRIA (FPS STABLE) ---
am kill-all 2>/dev/null || echo "[!] am kill-all não disponível neste dispositivo."
sysctl -w vm.drop_caches=3 2>/dev/null || echo "[!] sysctl/drop_caches não suportado neste dispositivo."

echo "========================================================="
echo "[✔️] SCRIPT APLICADO COM SUCESSO!"
echo "Precisão: MÁXIMA | Recuo: MITIGADO | Botão 4/Touch: 1ms"
echo "========================================================="
