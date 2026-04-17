#include <gtk/gtk.h>
#include <vte/vte.h>

static void run_neofetch(GtkWidget *terminal) {
    char **envp = g_get_environ();
    char **command = g_new0(char *, 2);
    command[0] = g_strdup("/app/bin/neofetch");
    command[1] = NULL;
    vte_terminal_spawn_async(VTE_TERMINAL(terminal), VTE_PTY_DEFAULT, NULL, command, envp, G_SPAWN_DEFAULT, NULL, NULL, NULL, -1, NULL, NULL, NULL);
    g_strfreev(envp);
    g_strfreev(command);
}

static void on_copy_clicked(GtkButton *btn, gpointer user_data) {
    VteTerminal *terminal = VTE_TERMINAL(user_data);
    vte_terminal_select_all(terminal);
    vte_terminal_copy_clipboard_format(terminal, VTE_FORMAT_TEXT);
    vte_terminal_unselect_all(terminal);
}

static void on_refresh_clicked(GtkButton *btn, gpointer user_data) {
    vte_terminal_reset(VTE_TERMINAL(user_data), TRUE, TRUE);
    run_neofetch(GTK_WIDGET(user_data));
}

static void activate(GtkApplication *app, gpointer user_data) {
    GtkSettings *settings = gtk_settings_get_default();
    g_object_set(settings, "gtk-application-prefer-dark-theme", TRUE, NULL);

    GtkWidget *window = gtk_application_window_new(app);
    gtk_window_set_title(GTK_WINDOW(window), "Neofetch GUI");
    gtk_window_set_default_size(GTK_WINDOW(window), 800, 500);

    GtkWidget *header = gtk_header_bar_new();
    gtk_window_set_titlebar(GTK_WINDOW(window), header);

    GtkWidget *terminal = vte_terminal_new();
    gtk_widget_set_margin_top(terminal, 20);
    gtk_widget_set_margin_bottom(terminal, 20);
    gtk_widget_set_margin_start(terminal, 20);
    gtk_widget_set_margin_end(terminal, 20);

    GdkRGBA foreground = {1.0, 1.0, 1.0, 1.0};
    GdkRGBA background = {0.02, 0.02, 0.02, 1.0};
    GdkRGBA palette[16] = {
        {0.0, 0.0, 0.0, 1.0}, {1.0, 0.0, 0.0, 1.0}, {0.0, 1.0, 0.0, 1.0}, {1.0, 1.0, 0.0, 1.0},
        {0.0, 0.0, 1.0, 1.0}, {1.0, 0.0, 1.0, 1.0}, {0.0, 1.0, 1.0, 1.0}, {0.9, 0.9, 0.9, 1.0},
        {0.2, 0.2, 0.2, 1.0}, {1.0, 0.2, 0.2, 1.0}, {0.2, 1.0, 0.2, 1.0}, {1.0, 1.0, 0.2, 1.0},
        {0.2, 0.2, 1.0, 1.0}, {1.0, 0.2, 1.0, 1.0}, {0.2, 1.0, 1.0, 1.0}, {1.0, 1.0, 1.0, 1.0}
    };
    vte_terminal_set_colors(VTE_TERMINAL(terminal), &foreground, &background, palette, 16);

    GtkWidget *refresh_btn = gtk_button_new_from_icon_name("view-refresh-symbolic");
    gtk_widget_set_tooltip_text(refresh_btn, "Refresh");
    g_signal_connect(refresh_btn, "clicked", G_CALLBACK(on_refresh_clicked), terminal);
    gtk_header_bar_pack_start(GTK_HEADER_BAR(header), refresh_btn);

    GtkWidget *copy_btn = gtk_button_new_from_icon_name("edit-copy-symbolic");
    gtk_widget_set_tooltip_text(copy_btn, "Copy to Clipboard");
    g_signal_connect(copy_btn, "clicked", G_CALLBACK(on_copy_clicked), terminal);
    gtk_header_bar_pack_start(GTK_HEADER_BAR(header), copy_btn);

    GtkCssProvider *provider = gtk_css_provider_new();
    gtk_css_provider_load_from_string(provider, "window { background-color: #0d0d0d; } headerbar { background-color: #1a1a1a; color: #ffffff; border-bottom: 2px solid #ff0000; }");
    gtk_style_context_add_provider_for_display(gdk_display_get_default(), GTK_STYLE_PROVIDER(provider), GTK_STYLE_PROVIDER_PRIORITY_APPLICATION);

    gtk_window_set_child(GTK_WINDOW(window), terminal);
    run_neofetch(terminal);
    gtk_window_present(GTK_WINDOW(window));
}

int main(int argc, char **argv) {
    GtkApplication *app = gtk_application_new("org.tiwut.NeofetchGui", G_APPLICATION_DEFAULT_FLAGS);
    g_signal_connect(app, "activate", G_CALLBACK(activate), NULL);
    return g_application_run(G_APPLICATION(app), argc, argv);
}
