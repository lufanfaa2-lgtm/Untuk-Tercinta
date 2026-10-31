local Rayfield = loadstring(game:HttpGet('https://githubusercontent.com'))()

-- Pembuatan Window/Menu Utama
local Window = Rayfield:CreateWindow({
   Name = "Maven’s Hub",
   LoadingTitle = "Load Skrip...",
   LoadingSubtitle = "Nacht Made ",
   ConfigurationSaving = { Enabled = false }
})

-- Membuat Tab Menu
local WebhookTab = Window:CreateTab("Webhook", 4483362458) -- ID Icon

-- Variabel Penyimpan Data URL Webhook
local URL_Webhook = ""

-- 1. Kotak Input untuk memasukkan URL Webhook
WebhookTab:CreateInput({
   Name = "Webhook Server Join / Leave URL",
   PlaceholderText = "Masukkan URL Webhook Discord di sini...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
       URL_Webhook = Text
   end,
})

-- 2. Tombol Toggle Aktif/Nonaktif Webhook Global
WebhookTab:CreateToggle({
   Name = "Send Webhook Global Join / Leave",
   CurrentValue = false,
   Flag = "ToggleWebhook", 
   Callback = function(Value)
       if Value then
           -- Logika ketika diaktifkan (OTOMATIS)
           print("Webhook Aktif dengan URL: " .. URL_Webhook)
           
           -- Mengirim data ke webhook discord ketika di-aktifkan
           if URL_Webhook ~= "" then
               local HttpService = game:GetService("HttpService")
               local data = {
                   ["content"] = "Pemain telah mengaktifkan log global dari game!"
               }
               pcall(function()
                   HttpService:PostAsync(URL_Webhook, HttpService:JSONEncode(data), Enum.HttpContentType.ApplicationJson)
               end)
           end
       else
           print("Webhook Dimatikan.")
       end
   end,
})
