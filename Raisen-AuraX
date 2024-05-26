--// leak

repeat wait() until game:IsLoaded()

game:GetService("CorePackages").Packages:Destroy()

assert(getrawmetatable)
grm = getrawmetatable(game)
setreadonly(grm, false)
old = grm.__namecall
grm.__namecall = newcclosure(function(self, ...)
    local args = {...}
    if tostring(args[1]) == "TeleportDetect" then
        return
    elseif tostring(args[1]) == "CHECKER_1" then
        return
    elseif tostring(args[1]) == "CHECKER" then
        return
    elseif tostring(args[1]) == "GUI_CHECK" then
        return
    elseif tostring(args[1]) == "OneMoreTime" then
        return
    elseif tostring(args[1]) == "checkingSPEED" then
        return
    elseif tostring(args[1]) == "BANREMOTE" then
        return
    elseif tostring(args[1]) == "PERMAIDBAN" then
        return
    elseif tostring(args[1]) == "KICKREMOTE" then
        return
    elseif tostring(args[1]) == "BR_KICKPC" then
        return
    elseif tostring(args[1]) == "BR_KICKMOBILE" then
        return
    end
    return old(self, ...)
end)

local library = { 
	flags = { }, 
	items = { } 
}

local players = game:GetService("Players")
local uis = game:GetService("UserInputService")
local runservice = game:GetService("RunService")
local tweenservice = game:GetService("TweenService")
local marketplaceservice = game:GetService("MarketplaceService")
local textservice = game:GetService("TextService")
local coregui = game:GetService("CoreGui")
local httpservice = game:GetService("HttpService")

local player = players.LocalPlayer
local mouse = player:GetMouse()
local camera = game.Workspace.CurrentCamera

library.theme = {
    fontsize = 17,
    titlesize = 18,
    font = Enum.Font.Code,
    background = "rbxassetid://0",
    tilesize = 90,
    cursor = false,
    cursorimg = "https://t0.rbxcdn.com/42f66da98c40252ee151326a82aab51f",
    backgroundcolor = Color3.fromRGB(20, 20, 20),
    tabstextcolor = Color3.fromRGB(168,122,207),
    bordercolor = Color3.fromRGB(75, 207, 255),
    accentcolor = Color3.fromRGB(168,122,207),
    accentcolor2 = Color3.fromRGB(88,65,108),
    outlinecolor = Color3.fromRGB(20,20,20),
    outlinecolor2 = Color3.fromRGB(30,30,30),--119, 64, 167
    sectorcolor = Color3.fromRGB(30, 30, 30),
    toptextcolor = Color3.fromRGB(255, 255, 255),
    topheight = 48,
    topcolor = Color3.fromRGB(30, 30, 30),
    topcolor2 = Color3.fromRGB(12,12,12), -- Color3.fromRGB(12, 12, 12),
    buttoncolor = Color3.fromRGB(49, 49, 49),
    buttoncolor2 = Color3.fromRGB(29,29,29),
    itemscolor = Color3.fromRGB(170, 170, 170),
    itemscolor2 = Color3.fromRGB(255,255,255)
}

if library.theme.cursor and Drawing then
    local success = pcall(function() 
        library.cursor = Drawing.new("Image")
        library.cursor.Data = game:HttpGet(library.theme.cursorimg)
        library.cursor.Size = Vector2.new(64, 64)
        library.cursor.Visible = uis.MouseEnabled
        library.cursor.Rounding = 0
        library.cursor.Position = Vector2.new(mouse.X - 32, mouse.Y + 6)
    end)
    if success and library.cursor then
        uis.InputChanged:Connect(function(input)
            if uis.MouseEnabled then
                if input.UserInputType == Enum.UserInputType.MouseMovement then
                    library.cursor.Position = Vector2.new(input.Position.X - 32, input.Position.Y + 7)
                end
            end
        end)
        
        game:GetService("RunService").RenderStepped:Connect(function()
            uis.OverrideMouseIconBehavior = Enum.OverrideMouseIconBehavior.ForceHide
            library.cursor.Visible = uis.MouseEnabled and (uis.MouseIconEnabled or game:GetService("GuiService").MenuIsOpen)
        end)
    elseif not success and library.cursor then
        library.cursor:Remove()
    end
end

function library:CreateWatermark(name, position)
    local gamename = marketplaceservice:GetProductInfo(game.PlaceId).Name
    local watermark = { }
    watermark.Visible = true
    watermark.text = " " .. name:gsub("{game}", gamename):gsub("{fps}", "0 FPS") .. " "

    watermark.main = Instance.new("ScreenGui", coregui)
    watermark.main.Name = "Watermark"
    if syn then
        syn.protect_gui(watermark.main)
    end

    if getgenv().watermark then
        getgenv().watermark:Remove()
    end
    getgenv().watermark = watermark.main
    
    watermark.mainbar = Instance.new("Frame", watermark.main)
    watermark.mainbar.Name = "Main"
    watermark.mainbar.BorderColor3 = Color3.fromRGB(80, 80, 80)
    watermark.mainbar.Visible = watermark.Visible
    watermark.mainbar.BorderSizePixel = 0
    watermark.mainbar.ZIndex = 5
    watermark.mainbar.Position = UDim2.new(0, position and position.X or 10, 0, position and position.Y or 10)
    watermark.mainbar.Size = UDim2.new(0, 0, 0, 25)

    watermark.Gradient = Instance.new("UIGradient", watermark.mainbar)
    watermark.Gradient.Rotation = 90
    watermark.Gradient.Color = ColorSequence.new({ ColorSequenceKeypoint.new(0.00, Color3.fromRGB(40, 40, 40)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(10, 10, 10)) })

    watermark.Outline = Instance.new("Frame", watermark.mainbar)
    watermark.Outline.Name = "outline"
    watermark.Outline.ZIndex = 4
    watermark.Outline.BorderSizePixel = 0
    watermark.Outline.Visible = watermark.Visible
    watermark.Outline.BackgroundColor3 = library.theme.outlinecolor
    watermark.Outline.Position = UDim2.fromOffset(-1, -1)

    watermark.BlackOutline = Instance.new("Frame", watermark.mainbar)
    watermark.BlackOutline.Name = "blackline"
    watermark.BlackOutline.ZIndex = 3
    watermark.BlackOutline.BorderSizePixel = 0
    watermark.BlackOutline.BackgroundColor3 = library.theme.outlinecolor2
    watermark.BlackOutline.Visible = watermark.Visible
    watermark.BlackOutline.Position = UDim2.fromOffset(-2, -2)

    watermark.label = Instance.new("TextLabel", watermark.mainbar)
    watermark.label.Name = "FPSLabel"
    watermark.label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    watermark.label.BackgroundTransparency = 1.000
    watermark.label.Position = UDim2.new(0, 0, 0, 0)
    watermark.label.Size = UDim2.new(0, 238, 0, 25)
    watermark.label.Font = library.theme.font
    watermark.label.ZIndex = 6
    watermark.label.Visible = watermark.Visible
    watermark.label.Text = watermark.text
    watermark.label.TextColor3 = Color3.fromRGB(255, 255, 255)
    watermark.label.TextSize = 15
    watermark.label.TextStrokeTransparency = 0.000
    watermark.label.TextXAlignment = Enum.TextXAlignment.Left
    watermark.label.Size = UDim2.new(0, watermark.label.TextBounds.X+10, 0, 25)
    
    watermark.topbar = Instance.new("Frame", watermark.mainbar)
    watermark.topbar.Name = "TopBar"
    watermark.topbar.ZIndex = 6
    watermark.topbar.BackgroundColor3 = library.theme.accentcolor
    watermark.topbar.BorderSizePixel = 0
    watermark.topbar.Visible = watermark.Visible
    watermark.topbar.Size = UDim2.new(0, 0, 0, 1)

    watermark.mainbar.Size = UDim2.new(0, watermark.label.TextBounds.X, 0, 25)
    watermark.topbar.Size = UDim2.new(0, watermark.label.TextBounds.X+6, 0, 1)
    watermark.Outline.Size = watermark.mainbar.Size + UDim2.fromOffset(2, 2)
    watermark.BlackOutline.Size = watermark.mainbar.Size + UDim2.fromOffset(4, 4)

    watermark.mainbar.Size = UDim2.new(0, watermark.label.TextBounds.X+4, 0, 25)    
    watermark.label.Size = UDim2.new(0, watermark.label.TextBounds.X+4, 0, 25)
    watermark.topbar.Size = UDim2.new(0, watermark.label.TextBounds.X+6, 0, 1)
    watermark.Outline.Size = watermark.mainbar.Size + UDim2.fromOffset(2, 2)
    watermark.BlackOutline.Size = watermark.mainbar.Size + UDim2.fromOffset(4, 4)

    local startTime, counter, oldfps = os.clock(), 0, nil
    runservice.Heartbeat:Connect(function()
        watermark.label.Visible = watermark.Visible
        watermark.mainbar.Visible = watermark.Visible
        watermark.topbar.Visible = watermark.Visible
        watermark.Outline.Visible = watermark.Visible
        watermark.BlackOutline.Visible = watermark.Visible

        if not name:find("{fps}") then
            watermark.label.Text = " " .. name:gsub("{game}", gamename):gsub("{fps}", "0 FPS") .. " "
        end

        if name:find("{fps}") then
            local currentTime = os.clock()
            counter = counter + 1
            if currentTime - startTime >= 1 then 
                local fps = math.floor(counter / (currentTime - startTime))
                counter = 0
                startTime = currentTime

                if fps ~= oldfps then
                    watermark.label.Text = " " .. name:gsub("{game}", gamename):gsub("{fps}", fps .. " FPS") .. " "
        
                    watermark.label.Size = UDim2.new(0, watermark.label.TextBounds.X+10, 0, 25)
                    watermark.mainbar.Size = UDim2.new(0, watermark.label.TextBounds.X, 0, 25)
                    watermark.topbar.Size = UDim2.new(0, watermark.label.TextBounds.X, 0, 1)

                    watermark.Outline.Size = watermark.mainbar.Size + UDim2.fromOffset(2, 2)
                    watermark.BlackOutline.Size = watermark.mainbar.Size + UDim2.fromOffset(4, 4)
                end
                oldfps = fps
            end
        end
    end)

    watermark.mainbar.MouseEnter:Connect(function()
        tweenservice:Create(watermark.mainbar, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 1, Active = false }):Play()
        tweenservice:Create(watermark.topbar, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 1, Active = false }):Play()
        tweenservice:Create(watermark.label, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { TextTransparency = 1, Active = false }):Play()
        tweenservice:Create(watermark.Outline, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 1, Active = false }):Play()
        tweenservice:Create(watermark.BlackOutline, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 1, Active = false }):Play()
    end)
    
    watermark.mainbar.MouseLeave:Connect(function()
        tweenservice:Create(watermark.mainbar, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 0, Active = true }):Play()
        tweenservice:Create(watermark.topbar, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 0, Active = true }):Play()
        tweenservice:Create(watermark.label, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { TextTransparency = 0, Active = true }):Play()
        tweenservice:Create(watermark.Outline, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 0, Active = true }):Play()
        tweenservice:Create(watermark.BlackOutline, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), { BackgroundTransparency = 0, Active = true }):Play()
    end)

    function watermark:UpdateTheme(theme)
        theme = theme or library.theme
        watermark.Outline.BackgroundColor3 = theme.outlinecolor
        watermark.BlackOutline.BackgroundColor3 = theme.outlinecolor2
        watermark.label.Font = theme.font
        watermark.topbar.BackgroundColor3 = theme.accentcolor
    end

    return watermark
end

function library:CreateWindow(name, size, hidebutton)
    local window = { }

    window.name = name or ""
    window.size = UDim2.fromOffset(size.X, size.Y) or UDim2.fromOffset(492, 598)
    window.hidebutton = hidebutton or Enum.KeyCode.RightShift
    window.theme = library.theme

    local updateevent = Instance.new("BindableEvent")
    function window:UpdateTheme(theme)
        updateevent:Fire(theme or library.theme)
        window.theme = (theme or library.theme)
    end

    window.Main = Instance.new("ScreenGui", coregui)
    window.Main.Name = name
    window.Main.DisplayOrder = 15
    if syn then
        syn.protect_gui(window.Main)
    end

    if getgenv().uilib then
        getgenv().uilib:Remove()
    end
    getgenv().uilib = window.Main

    local dragging, dragInput, dragStart, startPos
    uis.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            window.Frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)

    local dragstart = function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = window.Frame.Position
            
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end

    local dragend = function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end

    window.Frame = Instance.new("TextButton", window.Main)
    window.Frame.Name = "main"
    window.Frame.Position = UDim2.fromScale(0.5, 0.5)
    window.Frame.BorderSizePixel = 0
    window.Frame.Size = window.size
    window.Frame.AutoButtonColor = false
    window.Frame.Text = ""
    window.Frame.BackgroundColor3 = window.theme.backgroundcolor
    window.Frame.AnchorPoint = Vector2.new(0.5, 0.5)
    updateevent.Event:Connect(function(theme)
        window.Frame.BackgroundColor3 = theme.backgroundcolor
    end)

    uis.InputBegan:Connect(function(key)
        if key.KeyCode == window.hidebutton then
            window.Frame.Visible = not window.Frame.Visible
        end
    end)

    local function checkIfGuiInFront(Pos)
        local objects = coregui:GetGuiObjectsAtPosition(Pos.X, Pos.Y)
        for i,v in pairs(objects) do 
            if not string.find(v:GetFullName(), window.name) then 
                table.remove(objects, i)
            end 
        end
        return (#objects ~= 0 and objects[1].AbsolutePosition ~= Pos)
    end

    window.BlackOutline = Instance.new("Frame", window.Frame)
    window.BlackOutline.Name = "outline"
    window.BlackOutline.ZIndex = 1
    window.BlackOutline.Size = window.size + UDim2.fromOffset(2, 2)
    window.BlackOutline.BorderSizePixel = 0
    window.BlackOutline.BackgroundColor3 = window.theme.outlinecolor2
    window.BlackOutline.Position = UDim2.fromOffset(-1, -1)
    updateevent.Event:Connect(function(theme)
        window.BlackOutline.BackgroundColor3 = theme.outlinecolor2
    end)

    window.Outline = Instance.new("Frame", window.Frame)
    window.Outline.Name = "outline"
    window.Outline.ZIndex = 0
    window.Outline.Size = window.size + UDim2.fromOffset(4, 4)
    window.Outline.BorderSizePixel = 0
    window.Outline.BackgroundColor3 = window.theme.outlinecolor
    window.Outline.Position = UDim2.fromOffset(-2, -2)
    updateevent.Event:Connect(function(theme)
        window.Outline.BackgroundColor3 = theme.outlinecolor
    end)

    window.BlackOutline2 = Instance.new("Frame", window.Frame)
    window.BlackOutline2.Name = "outline"
    window.BlackOutline2.ZIndex = -1
    window.BlackOutline2.Size = window.size + UDim2.fromOffset(6, 6)
    window.BlackOutline2.BorderSizePixel = 0
    window.BlackOutline2.BackgroundColor3 = window.theme.outlinecolor2
    window.BlackOutline2.Position = UDim2.fromOffset(-3, -3)
    updateevent.Event:Connect(function(theme)
        window.BlackOutline2.BackgroundColor3 = theme.outlinecolor2
    end)

    window.TopBar = Instance.new("Frame", window.Frame)
    window.TopBar.Name = "top"
    window.TopBar.Size = UDim2.fromOffset(window.size.X.Offset, window.theme.topheight)
    window.TopBar.BorderSizePixel = 0
    window.TopBar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    window.TopBar.InputBegan:Connect(dragstart)
    window.TopBar.InputChanged:Connect(dragend)
    updateevent.Event:Connect(function(theme)
        window.TopBar.Size = UDim2.fromOffset(window.size.X.Offset, theme.topheight)
    end)

    window.TopGradient = Instance.new("UIGradient", window.TopBar)
    window.TopGradient.Rotation = 90
    window.TopGradient.Color = ColorSequence.new({ ColorSequenceKeypoint.new(0.00, window.theme.topcolor), ColorSequenceKeypoint.new(1.00, window.theme.topcolor2) })
    updateevent.Event:Connect(function(theme)
        window.TopGradient.Color = ColorSequence.new({ ColorSequenceKeypoint.new(0.00, theme.topcolor), ColorSequenceKeypoint.new(1.00, theme.topcolor2) })
    end)

    window.NameLabel = Instance.new("TextLabel", window.TopBar)
    window.NameLabel.TextColor3 = window.theme.toptextcolor
    window.NameLabel.Text = window.name
    window.NameLabel.TextXAlignment = Enum.TextXAlignment.Left
    window.NameLabel.Font = window.theme.font
    window.NameLabel.Name = "title"
    window.NameLabel.Position = UDim2.fromOffset(4, -2)
    window.NameLabel.BackgroundTransparency = 1
    window.NameLabel.Size = UDim2.fromOffset(190, window.TopBar.AbsoluteSize.Y / 2 - 2)
    window.NameLabel.TextSize = window.theme.titlesize
    updateevent.Event:Connect(function(theme)
        window.NameLabel.TextColor3 = theme.toptextcolor
        window.NameLabel.Font = theme.font
        window.NameLabel.TextSize = theme.titlesize
    end)

    window.Line2 = Instance.new("Frame", window.TopBar)
    window.Line2.Name = "line"
    window.Line2.Position = UDim2.fromOffset(0, window.TopBar.AbsoluteSize.Y / 2.1)
    window.Line2.Size = UDim2.fromOffset(window.size.X.Offset, 1)
    window.Line2.BorderSizePixel = 0
    window.Line2.BackgroundColor3 = window.theme.accentcolor
    updateevent.Event:Connect(function(theme)
        window.Line2.BackgroundColor3 = theme.accentcolor
    end)

    window.TabList = Instance.new("Frame", window.TopBar)
    window.TabList.Name = "tablist"
    window.TabList.BackgroundTransparency = 1
    window.TabList.Position = UDim2.fromOffset(0, window.TopBar.AbsoluteSize.Y / 2 + 1)
    window.TabList.Size = UDim2.fromOffset(window.size.X.Offset, window.TopBar.AbsoluteSize.Y / 2)
    window.TabList.BorderSizePixel = 0
    window.TabList.BackgroundColor3 = Color3.fromRGB(255, 255, 255)

    window.TabList.InputBegan:Connect(dragstart)
    window.TabList.InputChanged:Connect(dragend)

    window.BlackLine = Instance.new("Frame", window.Frame)
    window.BlackLine.Name = "blackline"
    window.BlackLine.Size = UDim2.fromOffset(window.size.X.Offset, 1)
    window.BlackLine.BorderSizePixel = 0
    window.BlackLine.ZIndex = 9
    window.BlackLine.BackgroundColor3 = window.theme.outlinecolor2
    window.BlackLine.Position = UDim2.fromOffset(0, window.TopBar.AbsoluteSize.Y)
    updateevent.Event:Connect(function(theme)
        window.BlackLine.BackgroundColor3 = theme.outlinecolor2
    end)

    window.BackgroundImage = Instance.new("ImageLabel", window.Frame)
    window.BackgroundImage.Name = "background"
    window.BackgroundImage.BorderSizePixel = 0
    window.BackgroundImage.ScaleType = Enum.ScaleType.Tile
    window.BackgroundImage.Position = window.BlackLine.Position + UDim2.fromOffset(0, 1)
    window.BackgroundImage.Size = UDim2.fromOffset(window.size.X.Offset, window.size.Y.Offset - window.TopBar.AbsoluteSize.Y - 1)
    window.BackgroundImage.Image = window.theme.background or ""
    window.BackgroundImage.ImageTransparency = window.BackgroundImage.Image ~= "" and 0 or 1
    window.BackgroundImage.ImageColor3 = Color3.new() 
    window.BackgroundImage.BackgroundColor3 = window.theme.backgroundcolor
    window.BackgroundImage.TileSize = UDim2.new(0, window.theme.tilesize, 0, window.theme.tilesize)
    updateevent.Event:Connect(function(theme)
        window.BackgroundImage.Image = theme.background or ""
        window.BackgroundImage.ImageTransparency = 
