local ts = game:GetService("TweenService")
local cg = game:GetService("CoreGui")
local copyfunc = setclipboard or toclipboard or set_clipboard or (Clipboard and Clipboard.set)

local gui = Instance.new("ScreenGui")
gui.Name = "ExpireAlert_" .. math.random(100, 999)
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true 

if syn and syn.protect_gui then
    syn.protect_gui(gui)
    gui.Parent = cg
elseif gethui then
    gui.Parent = gethui()
else
    gui.Parent = cg
end

local bg = Instance.new("Frame")
bg.Size = UDim2.new(1, 0, 1, 0)
bg.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
bg.BackgroundTransparency = 1
bg.BorderSizePixel = 0
bg.Parent = gui

ts:Create(bg, TweenInfo.new(0.5), {BackgroundTransparency = 0.6}):Play()

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 0, 0, 0)
main.Position = UDim2.new(0.5, 0, 0.5, 0)
main.AnchorPoint = Vector2.new(0.5, 0.5)
main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
main.BorderSizePixel = 0
main.ClipsDescendants = true
main.Parent = gui

Instance.new("UICorner", main).CornerRadius = UDim.new(0, 12)

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(255, 40, 40)
stroke.Thickness = 2
stroke.Parent = main

task.spawn(function()
    while main.Parent do
        ts:Create(stroke, TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 1}):Play()
        task.wait(0.8)
        ts:Create(stroke, TweenInfo.new(0.8, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 0}):Play()
        task.wait(0.8)
    end
end)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 60)
title.BackgroundTransparency = 1
title.Text = "⚠️ SCRIPT EXPIRED ⚠️"
title.TextColor3 = Color3.fromRGB(255, 60, 60)
title.Font = Enum.Font.GothamBlack
title.TextSize = 28
title.Parent = main

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.BackgroundTransparency = 1
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(150, 150, 150)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 18
closeBtn.Parent = main

closeBtn.MouseEnter:Connect(function()
    ts:Create(closeBtn, TweenInfo.new(0.2), {TextColor3 = Color3.fromRGB(255, 50, 50)}):Play()
end)

closeBtn.MouseLeave:Connect(function()
    ts:Create(closeBtn, TweenInfo.new(0.2), {TextColor3 = Color3.fromRGB(150, 150, 150)}):Play()
end)

closeBtn.MouseButton1Click:Connect(function()
    ts:Create(main, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Size = UDim2.new(0, 0, 0, 0)}):Play()
    ts:Create(bg, TweenInfo.new(0.4), {BackgroundTransparency = 1}):Play()
    task.wait(0.4)
    gui:Destroy()
end)

local msg = Instance.new("TextLabel")
msg.Size = UDim2.new(1, -40, 0, 80)
msg.Position = UDim2.new(0, 20, 0, 60)
msg.BackgroundTransparency = 1
msg.Text = "สคริปต์นี้หมดอายุการใช้งานแล้ว\nกรุณาติดต่อผู้พัฒนาเพื่อใช้งานต่อ\nDiscord: diablodeathangel | FaceBook: Diablø"
msg.TextColor3 = Color3.fromRGB(220, 220, 220)
msg.Font = Enum.Font.Gotham
msg.TextSize = 16
msg.TextWrapped = true
msg.Parent = main

local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0, 240, 0, 45)
btn.Position = UDim2.new(0.5, -120, 1, -65)
btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
btn.Text = "คัดลอกลิงก์ FaceBook"
btn.TextColor3 = Color3.fromRGB(255, 255, 255)
btn.Font = Enum.Font.GothamBold
btn.TextSize = 16
btn.AutoButtonColor = false
btn.Parent = main

Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)

local btnStroke = Instance.new("UIStroke")
btnStroke.Color = Color3.fromRGB(80, 80, 80)
btnStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
btnStroke.Parent = btn

btn.MouseEnter:Connect(function()
    ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(50, 50, 50)}):Play()
    ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(150, 150, 150)}):Play()
end)

btn.MouseLeave:Connect(function()
    ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(30, 30, 30)}):Play()
    ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(80, 80, 80)}):Play()
end)

btn.MouseButton1Click:Connect(function()
    if copyfunc then
        copyfunc("https://www.facebook.com/diabl.158225")
        btn.Text = "✅ คัดลอกสำเร็จ!"
        ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(40, 160, 60)}):Play()
        ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(60, 220, 80)}):Play()
        
        task.wait(2)
        btn.Text = "คัดลอกลิงก์ FaceBook"
        ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(50, 50, 50)}):Play()
        ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(150, 150, 150)}):Play()
    else
        btn.Text = "❌ Executor ไม่รองรับ!"
        ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(200, 50, 50)}):Play()
        ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(255, 100, 100)}):Play()
        
        task.wait(2)
        btn.Text = "คัดลอกลิงก์ FaceBook"
        ts:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(50, 50, 50)}):Play()
        ts:Create(btnStroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(150, 150, 150)}):Play()
    end
end)

ts:Create(main, TweenInfo.new(0.6, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Size = UDim2.new(0, 420, 0, 220)}):Play()
