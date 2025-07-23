<meta name='viewport' content='width=device-width, initial-scale=1'/>-- Detect executor
local executor = identifyexecutor and identifyexecutor():lower() or "unknown"
local isDelta = executor:find("delta")
local isKrnl = executor:find("krnl")

if isDelta then
    -- Fullscreen warning GUI
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "DeltaWarning"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.IgnoreGuiInset = true
    ScreenGui.Parent = game:GetService("CoreGui")

    local Frame = Instance.new("Frame")
    Frame.Parent = ScreenGui
    Frame.Size = UDim2.new(1, 0, 1, 0)
    Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)

    local TextLabel = Instance.new("TextLabel")
    TextLabel.Parent = Frame
    TextLabel.Text = "⚠ Delta Executor is considered unsafe and will not run this script.\n\nPlease use the trusted KRNL executor instead."
    TextLabel.Size = UDim2.new(1, -100, 0.4, 0)
    TextLabel.Position = UDim2.new(0, 50, 0.15, 0)
    TextLabel.BackgroundTransparency = 1
    TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    TextLabel.Font = Enum.Font.SourceSansBold
    TextLabel.TextScaled = true
    TextLabel.TextWrapped = true

    local CopyButton = Instance.new("TextButton")
    CopyButton.Parent = Frame
    CopyButton.Text = "Copy KRNL Link"
    CopyButton.Size = UDim2.new(0, 300, 0, 60)
    CopyButton.Position = UDim2.new(0.5, -150, 0.6, 0)
    CopyButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
    CopyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    CopyButton.Font = Enum.Font.SourceSansBold
    CopyButton.TextScaled = true

    CopyButton.MouseButton1Click:Connect(function()
        setclipboard("https://krnl.place/")
        CopyButton.Text = "Copied!"
    end)

    local Countdown = Instance.new("TextLabel")
    Countdown.Parent = Frame
    Countdown.Text = "Closing in 20 seconds..."
    Countdown.Size = UDim2.new(1, 0, 0, 50)
    Countdown.Position = UDim2.new(0, 0, 0.9, 0)
    Countdown.BackgroundTransparency = 1
    Countdown.Font = Enum.Font.SourceSansBold
    Countdown.TextColor3 = Color3.fromRGB(255, 0, 0)
    Countdown.TextScaled = true

    -- Countdown logic
    for i = 19, 0, -1 do
        task.wait(1)
        Countdown.Text = "Closing in " .. i .. " seconds..."
    end

    ScreenGui:Destroy()

elseif isKrnl then
    -- Run actual script if KRNL is used
    loadstring(game:HttpGet("https://raw.githubusercontent.com/NoIag-id/No-Lag-HUB/refs/heads/main/LoaderV2.lua"))()
    warn("Unsupported executor. This script is intended for KRNL.")
end
