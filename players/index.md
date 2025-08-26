package com.tunombre; // ¡Cambia esto por tu paquete!

import net.fabricmc.fabric.api.client.rendering.v1.HudRenderCallback;
import net.minecraft.client.MinecraftClient;
import net.minecraft.client.font.TextRenderer;
import net.minecraft.client.util.math.MatrixStack;
import net.minecraft.text.Text;

public class CoordinatesHUD {
    // Método para registrar nuestro HUD
    public static void register() {
        HudRenderCallback.EVENT.register((matrixStack, tickDelta) -> {
            renderCoordinates(matrixStack);
        });
    }

    private static void renderCoordinates(MatrixStack matrixStack) {
        // Obtiene el cliente de Minecraft y el renderizador de texto
        MinecraftClient client = MinecraftClient.getInstance();
        TextRenderer textRenderer = client.textRenderer;

        // Asegurarse de que estamos en un mundo y de que el jugador existe
        if (client.player == null || client.world == null) return;

        // Obtener las coordenadas del jugador
        int x = (int) client.player.getX();
        int y = (int) client.player.getY();
        int z = (int) client.player.getZ();

        // Formatear el texto a mostrar
        String coordsText = String.format("XYZ: %d, %d, %d", x, y, z);

        // Dibujar el texto en la pantalla (esquina superior izquierda)
        int screenHeight = client.getWindow().getScaledHeight();
        int textWidth = textRenderer.getWidth(coordsText);
        int xPos = 5; // 5 píxeles desde el borde izquierdo
        int yPos = 5; // 5 píxeles desde el borde superior

        // Fondo semi-transparente para mejor legibilidad
        int padding = 2;
        fill(matrixStack, xPos - padding, yPos - padding, xPos + textWidth + padding, yPos + 9 + padding, 0x80000000);

        // Dibujar el texto blanco
        textRenderer.drawWithShadow(matrixStack, coordsText, xPos, yPos, 0xFFFFFF); // 0xFFFFFF es color blanco
    }

    // Método auxiliar para dibujar un rectángulo relleno (para el fondo)
    private static void fill(MatrixStack matrices, int x1, int y1, int x2, int y2, int color) {
        net.minecraft.client.gui.DrawableHelper.fill(matrices, x1, y1, x2, y2, color);
    }
}
