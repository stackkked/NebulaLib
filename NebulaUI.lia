--[[
╔══════════════════════════════════════════════════════════════╗
║                    NebulaLib  v1.0.0                         ║
║           Roblox Executor UI Library                         ║
╠══════════════════════════════════════════════════════════════╣
║  ИКОНКИ (скачай и положи в папку icons/ рядом с либой):     ║
║  https://www.flaticon.com/free-icon/sword_2917242            ║
║  https://www.flaticon.com/free-icon/eye_709612               ║
║  https://www.flaticon.com/free-icon/settings_3524659         ║
║  https://www.flaticon.com/free-icon/person_1077012           ║
║  https://www.flaticon.com/free-icon/gamepad_686589           ║
║  https://www.flaticon.com/free-icon/shield_992651            ║
║  https://www.flaticon.com/free-icon/lightning_3163478        ║
║  https://www.flaticon.com/free-icon/target_1085795           ║
║  ИЛИ используй rbxassetid:// напрямую в поле Icon            ║
╠══════════════════════════════════════════════════════════════╣
║  БЫСТРЫЙ СТАРТ:                                              ║
║                                                              ║
║  local Nebula = loadstring(game:HttpGet("RAW_URL"))()        ║
║                                                              ║
║  local Win = Nebula:CreateWindow({                           ║
║      Title          = "MyScript",                            ║
║      Subtitle       = "v1.0",                                ║
║      ToggleKey      = Enum.KeyCode.RightShift,               ║
║      NotifyPosition = "TopRight",                            ║
║  })                                                          ║
║                                                              ║
║  local Tab = Win:AddTab({                                    ║
║      Name = "Combat",                                        ║
║      Icon = "rbxassetid://7733960981",                       ║
║  })                                                          ║
║                                                              ║
║  Tab:Toggle({                                                ║
║      Name     = "Aimbot",                                    ║
║      Default  = false,                                       ║
║      Key      = Enum.KeyCode.E,                              ║
║      KeyMode  = "Toggle",  -- "Toggle" или "Hold"            ║
║      Callback = function(v) print("Aimbot:", v) end,         ║
║  })                                                          ║
║                                                              ║
║  Tab:Slider({                                                ║
║      Name     = "FOV",                                       ║
║      Min = 0, Max = 360, Default = 90,                       ║
║      Suffix   = "°",                                         ║
║      Callback = function(v) end,                             ║
║  })                                                          ║
║                                                              ║
║  Tab:Dropdown({                                              ║
║      Name    = "Targets",                                    ║
║      Options = {"Players","NPCs","Bosses"},                  ║
║      Multi   = true,                                         ║
║      Default = {"Players"},                                  ║
║      Callback = function(v) end,                             ║
║  })                                                          ║
║                                                              ║
║  Tab:Keybind({                                               ║
║      Name = "Fly", Key = Enum.KeyCode.F,                     ║
║      Mode = "Toggle",                                        ║
║      Callback = function(active) end,                        ║
║  })                                                          ║
║                                                              ║
║  Tab:Button({ Name="Run", Callback=function() end })         ║
║  Tab:Input({ Name="Prefix", Placeholder=";" })               ║
║  Tab:Label({ Text="Section" })                               ║
║  Tab:Separator()                                             ║
║                                                              ║
║  Win:Notify({                                                ║
║      Title    = "Loaded!",                                   ║
║      Message  = "All good.",                                 ║
║      Type     = "success",  -- info/success/warning/error    ║
║      Duration = 4,                                           ║
║  })                                                          ║
╚══════════════════════════════════════════════════════════════╝
]]

-- ─────────────────────────────────────────────
--  Services
-- ─────────────────────────────────────────────
local Players          = game:GetService("Players")
local UIS              = game:GetService("UserInputService")
local TweenService     = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer

-- ─────────────────────────────────────────────
--  Theme
-- ─────────────────────────────────────────────
local T = {
    -- Backgrounds
    BG0 = Color3.fromHex("08080e"),
    BG1 = Color3.fromHex("0f0f17"),
    BG2 = Color3.fromHex("16161f"),
    BG3 = Color3.fromHex("1c1c27"),
    BG4 = Color3.fromHex("22222e"),
    BG5 = Color3.fromHex("2a2a38"),

    -- Accent purple
    Acc  = Color3.fromHex("7c6af7"),
    Acc2 = Color3.fromHex("a78bfa"),
    AccD = Color3.fromHex("3d3578"), -- dark accent for fills

    -- Text
    T1 = Color3.fromHex("f0f0ff"),
    T2 = Color3.fromHex("b0b0cc"),
    T3 = Color3.fromHex("6a6a88"),

    -- Semantic
    Red   = Color3.fromHex("f87171"),
    Green = Color3.fromHex("4ade80"),
    Amber = Color3.fromHex("fbbf24"),
    Blue  = Color3.fromHex("60a5fa"),

    -- Borders (use with Transparency)
    Brd  = Color3.fromRGB(255,255,255),
    BrdA = Color3.fromHex("7c6af7"),

    -- Fonts
    FB = Enum.Font.GothamBold,
    FS = Enum.Font.GothamSemibold,
    FM = Enum.Font.Gotham,

    -- Radii
    CR  = UDim.new(0,8),
    CRL = UDim.new(0,12),
    CRR = UDim.new(0,20),
}

-- ─────────────────────────────────────────────
--  Helpers
-- ─────────────────────────────────────────────
local function Tw(obj, props, t, style)
    TweenService:Create(obj,
        TweenInfo.new(t or .18, style or Enum.EasingStyle.Quint),
        props):Play()
end

local function New(cls, p, par)
    local o = Instance.new(cls)
    for k,v in pairs(p or {}) do o[k]=v end
    if par then o.Parent=par end
    return o
end

local function Corner(par, r)
    return New("UICorner",{CornerRadius=r or T.CR},par)
end

local function Stroke(par, col, tr, th)
    return New("UIStroke",{
        Color=col or T.Brd, Transparency=tr or .9,
        Thickness=th or 1,
        ApplyStrokeMode=Enum.ApplyStrokeMode.Border,
    },par)
end

local function Pad(par, t,r,b,l)
    return New("UIPadding",{
        PaddingTop=UDim.new(0,t or 0), PaddingRight=UDim.new(0,r or 0),
        PaddingBottom=UDim.new(0,b or 0), PaddingLeft=UDim.new(0,l or 0),
    },par)
end

local function List(par, dir, ha, sp)
    local l = New("UIListLayout",{
        FillDirection       = dir or Enum.FillDirection.Vertical,
        HorizontalAlignment = ha  or Enum.HorizontalAlignment.Left,
        SortOrder           = Enum.SortOrder.LayoutOrder,
        Padding             = UDim.new(0,sp or 6),
    },par)
    l:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        if par:IsA("ScrollingFrame") then
            par.CanvasSize = UDim2.new(0,0,0,l.AbsoluteContentSize.Y+12)
        end
    end)
    return l
end

local function Lbl(par, txt, sz, col, fnt, xa)
    return New("TextLabel",{
        Text=txt or "", TextSize=sz or 14,
        TextColor3=col or T.T1, Font=fnt or T.FM,
        TextXAlignment=xa or Enum.TextXAlignment.Left,
        BackgroundTransparency=1,
        Size=UDim2.new(1,0,0,sz and sz+4 or 18),
    },par)
end

-- Key name map
local KN = {
    [Enum.KeyCode.LeftShift]="LShift",[Enum.KeyCode.RightShift]="RShift",
    [Enum.KeyCode.LeftControl]="LCtrl",[Enum.KeyCode.RightControl]="RCtrl",
    [Enum.KeyCode.LeftAlt]="LAlt",[Enum.KeyCode.RightAlt]="RAlt",
    [Enum.KeyCode.Return]="Enter",[Enum.KeyCode.BackSpace]="Bksp",
    [Enum.KeyCode.Space]="Space",[Enum.KeyCode.CapsLock]="Caps",
    [Enum.KeyCode.Tab]="Tab",[Enum.KeyCode.Delete]="Del",
    [Enum.KeyCode.F1]="F1",[Enum.KeyCode.F2]="F2",[Enum.KeyCode.F3]="F3",
    [Enum.KeyCode.F4]="F4",[Enum.KeyCode.F5]="F5",[Enum.KeyCode.F6]="F6",
    [Enum.KeyCode.F7]="F7",[Enum.KeyCode.F8]="F8",[Enum.KeyCode.F9]="F9",
    [Enum.KeyCode.F10]="F10",[Enum.KeyCode.F11]="F11",[Enum.KeyCode.F12]="F12",
}
local function KName(kc) return kc and (KN[kc] or kc.Name) or "None" end

-- Drag
local function Drag(handle, frame)
    local drag,di,mp,fp
    handle.InputBegan:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.MouseButton1 then
            drag=true; mp=i.Position; fp=frame.Position
            i.Changed:Connect(function()
                if i.UserInputState==Enum.UserInputState.End then drag=false end
            end)
        end
    end)
    handle.InputChanged:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.MouseMovement then di=i end
    end)
    UIS.InputChanged:Connect(function(i)
        if i==di and drag then
            local d=i.Position-mp
            frame.Position=UDim2.new(fp.X.Scale,fp.X.Offset+d.X,fp.Y.Scale,fp.Y.Offset+d.Y)
        end
    end)
end

-- ScreenGui
local function MakeGui(name)
    local sg=Instance.new("ScreenGui")
    sg.Name=name; sg.ResetOnSpawn=false
    sg.ZIndexBehavior=Enum.ZIndexBehavior.Sibling
    sg.IgnoreGuiInset=true
    local ok=pcall(function() sg.Parent=game:GetService("CoreGui") end)
    if not ok then sg.Parent=LocalPlayer:WaitForChild("PlayerGui") end
    return sg
end

-- ══════════════════════════════════════════════
--  NEBULA LIBRARY
-- ══════════════════════════════════════════════
local Nebula = {}
Nebula.__index = Nebula

function Nebula:CreateWindow(cfg)
    cfg = cfg or {}
    local title     = cfg.Title         or "Nebula"
    local subtitle  = cfg.Subtitle      or "v1.0"
    local tKey      = cfg.ToggleKey     or Enum.KeyCode.RightShift
    local nPos      = cfg.NotifyPosition or "TopRight"

    local W = setmetatable({
        _tabs={}; _active=nil; _conns={}; _visible=false; _indicators={};
    },{__index=self})

    W.Gui = MakeGui("NebulaLib_"..title)

    -- ══════════════════════════════
    --  NOTIFICATION SYSTEM
    -- ══════════════════════════════
    local nAnchors = {
        TopRight    = {ap=Vector2.new(1,0), pos=UDim2.new(1,-16,0,16),   va=Enum.VerticalAlignment.Top,    ha=Enum.HorizontalAlignment.Right},
        TopLeft     = {ap=Vector2.new(0,0), pos=UDim2.new(0,16,0,16),    va=Enum.VerticalAlignment.Top,    ha=Enum.HorizontalAlignment.Left},
        BottomRight = {ap=Vector2.new(1,1), pos=UDim2.new(1,-16,1,-16),  va=Enum.VerticalAlignment.Bottom, ha=Enum.HorizontalAlignment.Right},
        BottomLeft  = {ap=Vector2.new(0,1), pos=UDim2.new(0,16,1,-16),   va=Enum.VerticalAlignment.Bottom, ha=Enum.HorizontalAlignment.Left},
    }
    local na = nAnchors[nPos] or nAnchors.TopRight

    W.NotifHolder = New("Frame",{
        Name="NotifHolder",
        Size=UDim2.new(0,290,0,600),
        Position=na.pos, AnchorPoint=na.ap,
        BackgroundTransparency=1, ZIndex=200,
    },W.Gui)
    New("UIListLayout",{
        FillDirection=Enum.FillDirection.Vertical,
        HorizontalAlignment=na.ha,
        VerticalAlignment=na.va,
        SortOrder=Enum.SortOrder.LayoutOrder,
        Padding=UDim.new(0,6),
    },W.NotifHolder)

    -- ══════════════════════════════
    --  KEYBIND INDICATOR (bottom)
    -- ══════════════════════════════
    W.IndHolder = New("Frame",{
        Name="IndicatorHolder",
        Size=UDim2.new(0,600,0,32),
        Position=UDim2.new(0.5,0,1,-50),
        AnchorPoint=Vector2.new(0.5,0),
        BackgroundTransparency=1, ZIndex=150,
    },W.Gui)
    New("UIListLayout",{
        FillDirection=Enum.FillDirection.Horizontal,
        HorizontalAlignment=Enum.HorizontalAlignment.Center,
        VerticalAlignment=Enum.VerticalAlignment.Center,
        SortOrder=Enum.SortOrder.LayoutOrder,
        Padding=UDim.new(0,6),
    },W.IndHolder)

    -- ══════════════════════════════
    --  TOP BAR  (heart + title)
    -- ══════════════════════════════
    W.TopBar = New("Frame",{
        Name="TopBar",
        Size=UDim2.new(0,0,0,42),
        AutomaticSize=Enum.AutomaticSize.X,
        Position=UDim2.new(0.5,0,0,14),
        AnchorPoint=Vector2.new(0.5,0),
        BackgroundColor3=T.BG2, ZIndex=60,
    },W.Gui)
    Corner(W.TopBar,T.CRR)
    Stroke(W.TopBar,T.BrdA,0.55,1)
    Pad(W.TopBar,0,16,0,8)

    New("UIListLayout",{
        FillDirection=Enum.FillDirection.Horizontal,
        VerticalAlignment=Enum.VerticalAlignment.Center,
        SortOrder=Enum.SortOrder.LayoutOrder,
        Padding=UDim.new(0,10),
    },W.TopBar)

    -- heart circle
    local heartCircle = New("Frame",{
        Size=UDim2.new(0,30,0,30),
        BackgroundColor3=T.Acc, ZIndex=62,
        LayoutOrder=0,
    },W.TopBar)
    Corner(heartCircle,UDim.new(1,0))
    -- glow
    New("ImageLabel",{
        Image="rbxassetid://5028857084",
        Size=UDim2.new(0,52,0,52),
        Position=UDim2.new(0.5,0,0.5,0),
        AnchorPoint=Vector2.new(0.5,0.5),
        BackgroundTransparency=1,
        ImageColor3=T.Acc, ImageTransparency=0.55,
        ZIndex=61,
    },heartCircle)
    New("TextLabel",{
        Text="♥", TextSize=14,
        TextColor3=Color3.new(1,1,1),
        Font=T.FB, Size=UDim2.new(1,0,1,0),
        BackgroundTransparency=1,
        TextXAlignment=Enum.TextXAlignment.Center,
        TextYAlignment=Enum.TextYAlignment.Center,
        ZIndex=63,
    },heartCircle)

    -- divider
    New("Frame",{
        Size=UDim2.new(0,1,0,22),
        BackgroundColor3=T.Brd,
        BackgroundTransparency=0.86,
        BorderSizePixel=0,
        LayoutOrder=1,
    },W.TopBar)

    -- title
    local titleLbl = New("TextLabel",{
        Text=title,
        TextSize=15, TextColor3=T.T1,
        Font=T.FB,
        Size=UDim2.new(0,0,0,22),
        AutomaticSize=Enum.AutomaticSize.X,
        BackgroundTransparency=1,
        TextXAlignment=Enum.TextXAlignment.Left,
        ZIndex=62, LayoutOrder=2,
    },W.TopBar)

    -- subtitle badge
    local subBg = New("Frame",{
        Size=UDim2.new(0,0,0,20),
        AutomaticSize=Enum.AutomaticSize.X,
        BackgroundColor3=T.AccD,
        ZIndex=62, LayoutOrder=3,
    },W.TopBar)
    Corner(subBg,UDim.new(0,10))
    Stroke(subBg,T.BrdA,0.5,1)
    Pad(subBg,0,8,0,8)
    New("TextLabel",{
        Text=subtitle, TextSize=11,
        TextColor3=T.Acc2, Font=T.FB,
        Size=UDim2.new(0,0,1,0),
        AutomaticSize=Enum.AutomaticSize.X,
        BackgroundTransparency=1,
        TextXAlignment=Enum.TextXAlignment.Center,
        ZIndex=63,
    },subBg)

    Drag(W.TopBar,W.TopBar)

    -- ══════════════════════════════
    --  MAIN WINDOW
    -- ══════════════════════════════
    W.Win = New("Frame",{
        Name="MainWindow",
        Size=UDim2.new(0,580,0,420),
        Position=UDim2.new(0.5,0,0.5,0),
        AnchorPoint=Vector2.new(0.5,0.5),
        BackgroundColor3=T.BG1,
        ClipsDescendants=true,
        Visible=false, ZIndex=50,
    },W.Gui)
    Corner(W.Win,T.CRL)
    Stroke(W.Win,T.BrdA,0.6,1)

    -- title bar
    local winBar = New("Frame",{
        Size=UDim2.new(1,0,0,46),
        BackgroundColor3=T.BG2,
        ZIndex=52,
    },W.Win)
    New("UIGradient",{
        Color=ColorSequence.new({
            ColorSequenceKeypoint.new(0,T.BG2),
            ColorSequenceKeypoint.new(1,T.BG3),
        }),Rotation=90,
    },winBar)
    New("Frame",{
        Size=UDim2.new(1,0,0,1),Position=UDim2.new(0,0,1,0),
        BackgroundColor3=T.BrdA,BackgroundTransparency=0.65,
        BorderSizePixel=0,ZIndex=53,
    },winBar)

    -- accent dot
    local dot=New("Frame",{
        Size=UDim2.new(0,8,0,8),
        Position=UDim2.new(0,14,0.5,0),
        AnchorPoint=Vector2.new(0,0.5),
        BackgroundColor3=T.Acc,ZIndex=54,
    },winBar)
    Corner(dot,UDim.new(1,0))
    New("ImageLabel",{
        Image="rbxassetid://5028857084",
        Size=UDim2.new(0,20,0,20),
        Position=UDim2.new(0.5,0,0.5,0),
        AnchorPoint=Vector2.new(0.5,0.5),
        BackgroundTransparency=1,
        ImageColor3=T.Acc,ImageTransparency=0.5,ZIndex=53,
    },dot)

    New("TextLabel",{
        Text=title,TextSize=14,TextColor3=T.T1,Font=T.FB,
        Size=UDim2.new(1,-100,1,0),Position=UDim2.new(0,30,0,0),
        BackgroundTransparency=1,TextXAlignment=Enum.TextXAlignment.Left,
        ZIndex=54,
    },winBar)

    -- close & minimize
    local function WBtn(xOff, col, txt, cb)
        local b=New("TextButton",{
            Size=UDim2.new(0,22,0,22),
            Position=UDim2.new(1,xOff,0.5,0),
            AnchorPoint=Vector2.new(1,0.5),
            BackgroundColor3=col, BackgroundTransparency=0.65,
            Text=txt, TextSize=11, TextColor3=col,
            Font=T.FB, ZIndex=55,
        },winBar)
        Corner(b,UDim.new(1,0))
        b.MouseEnter:Connect(function() Tw(b,{BackgroundTransparency=0.25},.1) end)
        b.MouseLeave:Connect(function() Tw(b,{BackgroundTransparency=0.65},.1) end)
        b.Activated:Connect(cb); return b
    end
    WBtn(-10,T.Red,"×",function()
        Tw(W.Win,{GroupTransparency=1},.15)
        task.delay(.16,function() W.Win.Visible=false end)
        W._visible=false
    end)
    WBtn(-38,T.Amber,"–",function()
        Tw(W.Win,{GroupTransparency=1},.15)
        task.delay(.16,function() W.Win.Visible=false end)
        W._visible=false
    end)

    Drag(winBar,W.Win)

    -- ── Tab Sidebar (RIGHT side) ───────────────
    W.TabBar = New("Frame",{
        Name="TabSidebar",
        Size=UDim2.new(0,56,1,-46),
        Position=UDim2.new(1,0,0,46),
        AnchorPoint=Vector2.new(1,0),
        BackgroundColor3=T.BG2, ZIndex=52,
    },W.Win)
    New("Frame",{
        Size=UDim2.new(0,1,1,0),
        BackgroundColor3=T.Brd,
        BackgroundTransparency=0.87,
        BorderSizePixel=0,ZIndex=53,
    },W.TabBar)

    local tabListFrame = New("Frame",{
        Size=UDim2.new(1,0,1,0),
        BackgroundTransparency=1, ZIndex=53,
    },W.TabBar)
    List(tabListFrame,Enum.FillDirection.Vertical,Enum.HorizontalAlignment.Center,4)
    Pad(tabListFrame,8,0,8,0)

    -- ── Content area ──────────────────────────
    W.ContentArea = New("Frame",{
        Name="ContentArea",
        Size=UDim2.new(1,-56,1,-46),
        Position=UDim2.new(0,0,0,46),
        BackgroundTransparency=1,
        ClipsDescendants=true, ZIndex=51,
    },W.Win)

    -- ── Toggle window on key ──────────────────
    table.insert(W._conns, UIS.InputBegan:Connect(function(inp, gpe)
        if gpe then return end
        if inp.KeyCode == tKey then
            W._visible = not W._visible
            if W._visible then
                W.Win.GroupTransparency=1
                W.Win.Visible=true
                Tw(W.Win,{GroupTransparency=0},.22,Enum.EasingStyle.Back)
            else
                Tw(W.Win,{GroupTransparency=1},.18)
                task.delay(.2,function() W.Win.Visible=false end)
            end
        end
    end))

    -- ══════════════════════════════════════════
    --  Notify method
    -- ══════════════════════════════════════════
    function W:Notify(c)
        c = c or {}
        local nt   = c.Type or "info"
        local dur  = c.Duration or 4
        local cols = {info=T.Blue, success=T.Green, warning=T.Amber, error=T.Red}
        local acc  = cols[nt] or T.Blue
        local icons= {info="ℹ", success="✔", warning="⚠", error="✖"}

        local card = New("Frame",{
            Size=UDim2.new(1,0,0,64),
            BackgroundColor3=T.BG3,
            ZIndex=201, ClipsDescendants=true,
        },self.NotifHolder)
        Corner(card,UDim.new(0,10))
        Stroke(card,acc,0.45,1)

        -- left bar
        New("Frame",{
            Size=UDim2.new(0,3,1,0),
            BackgroundColor3=acc,
            BorderSizePixel=0,ZIndex=202,
        },card)
        Corner(New("Frame",{Size=UDim2.new(0,3,1,0),BackgroundColor3=acc,BorderSizePixel=0,ZIndex=202},card),UDim.new(0,2))

        local inner=New("Frame",{
            Size=UDim2.new(1,-6,1,0),
            Position=UDim2.new(0,6,0,0),
            BackgroundTransparency=1,ZIndex=202,
        },card)
        Pad(inner,8,10,8,8)

        -- icon
        New("TextLabel",{
            Text=icons[nt] or "ℹ",
            TextSize=13,TextColor3=acc,Font=T.FB,
            Size=UDim2.new(0,18,0,16),
            BackgroundTransparency=1,
            TextXAlignment=Enum.TextXAlignment.Center,
            ZIndex=203,
        },inner)

        local tl=New("TextLabel",{
            Text=c.Title or "Notification",
            TextSize=13,TextColor3=T.T1,Font=T.FB,
            Size=UDim2.new(1,-22,0,16),
            Position=UDim2.new(0,22,0,0),
            BackgroundTransparency=1,
            TextXAlignment=Enum.TextXAlignment.Left,
            ZIndex=203,
        },inner)

        New("TextLabel",{
            Text=c.Message or "",
            TextSize=12,TextColor3=T.T2,Font=T.FM,
            Size=UDim2.new(1,0,0,14),
            Position=UDim2.new(0,0,0,20),
            BackgroundTransparency=1,
            TextXAlignment=Enum.TextXAlignment.Left,
            TextWrapped=true, ZIndex=203,
        },inner)

        -- progress strip
        local bar=New("Frame",{
            Size=UDim2.new(1,0,0,2),
            Position=UDim2.new(0,0,1,-2),
            BackgroundColor3=acc,
            BackgroundTransparency=0.3,
            BorderSizePixel=0, ZIndex=203,
        },card)
        Tw(bar,{Size=UDim2.new(0,0,0,2)},dur,Enum.EasingStyle.Linear)

        -- slide in from correct side
        local isRight = nPos:find("Right") ~= nil
        card.Position = UDim2.new(isRight and 1.1 or -0.1, 0, 0, 0)
        Tw(card,{Position=UDim2.new(0,0,0,0)},.3,Enum.EasingStyle.Back)

        task.delay(dur, function()
            Tw(card,{Position=UDim2.new(isRight and 1.1 or -0.1,0,0,0)},.25)
            task.wait(.28)
            card:Destroy()
        end)
    end

    -- ══════════════════════════════════════════
    --  Keybind indicator (bottom centre)
    -- ══════════════════════════════════════════
    function W:_SetInd(name, active)
        if self._indicators[name] then
            self._indicators[name]:Destroy()
            self._indicators[name]=nil
        end
        if not active then return end

        local pill=New("Frame",{
            Size=UDim2.new(0,0,0,26),
            AutomaticSize=Enum.AutomaticSize.X,
            BackgroundColor3=T.BG3,
            BackgroundTransparency=0,
            ZIndex=151,
        },self.IndHolder)
        Corner(pill,UDim.new(0,13))
        Stroke(pill,T.BrdA,0.45,1)

        local ip=New("Frame",{
            Size=UDim2.new(0,0,1,0),
            AutomaticSize=Enum.AutomaticSize.X,
            BackgroundTransparency=1,ZIndex=152,
        },pill)
        Pad(ip,0,10,0,10)
        New("UIListLayout",{
            FillDirection=Enum.FillDirection.Horizontal,
            VerticalAlignment=Enum.VerticalAlignment.Center,
            SortOrder=Enum.SortOrder.LayoutOrder,
            Padding=UDim.new(0,5),
        },ip)

        local d=New("Frame",{
            Size=UDim2.new(0,6,0,6),
            BackgroundColor3=T.Green,
            LayoutOrder=0,ZIndex=153,
        },ip)
        Corner(d,UDim.new(1,0))
        New("ImageLabel",{
            Image="rbxassetid://5028857084",
            Size=UDim2.new(0,14,0,14),
            Position=UDim2.new(0.5,0,0.5,0),
            AnchorPoint=Vector2.new(0.5,0.5),
            BackgroundTransparency=1,
            ImageColor3=T.Green,ImageTransparency=0.45,
            ZIndex=152,
        },d)

        New("TextLabel",{
            Text=name, TextSize=11, TextColor3=T.T2,
            Font=T.FM, Size=UDim2.new(0,#name*6.5,0,20),
            BackgroundTransparency=1,
            TextXAlignment=Enum.TextXAlignment.Left,
            LayoutOrder=1,ZIndex=153,
        },ip)

        self._indicators[name]=pill

        -- pulse animation
        task.spawn(function()
            while self._indicators[name] do
                Tw(d,{BackgroundTransparency=0.3},.5)
                task.wait(.5)
                Tw(d,{BackgroundTransparency=0},.5)
                task.wait(.5)
            end
        end)
    end

    -- ══════════════════════════════════════════
    --  AddTab
    -- ══════════════════════════════════════════
    function W:AddTab(cfg2)
        cfg2 = cfg2 or {}
        local tName = cfg2.Name or ("Tab "..#self._tabs+1)
        local tIcon = cfg2.Icon or ""

        -- sidebar button
        local btn=New("TextButton",{
            Size=UDim2.new(0,42,0,42),
            BackgroundColor3=T.BG3,
            BackgroundTransparency=1,
            Text="", ZIndex=54,
        },tabListFrame)
        Corner(btn,UDim.new(0,10))

        -- icon or letter
        if tIcon~="" then
            New("ImageLabel",{
                Image=tIcon,
                Size=UDim2.new(0,22,0,22),
                Position=UDim2.new(0.5,0,0.5,0),
                AnchorPoint=Vector2.new(0.5,0.5),
                BackgroundTransparency=1,
                ImageColor3=T.T3,
                ZIndex=55, Name="Icon",
            },btn)
        else
            New("TextLabel",{
                Text=tName:sub(1,1):upper(),
                TextSize=17,TextColor3=T.T3,Font=T.FB,
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,
                TextXAlignment=Enum.TextXAlignment.Center,
                TextYAlignment=Enum.TextYAlignment.Center,
                ZIndex=55, Name="Icon",
            },btn)
        end

        -- active side line
        local sideLine=New("Frame",{
            Size=UDim2.new(0,3,0,0),
            Position=UDim2.new(0,-7,0.5,0),
            AnchorPoint=Vector2.new(0,0.5),
            BackgroundColor3=T.Acc,
            BackgroundTransparency=1,
            BorderSizePixel=0, ZIndex=55,
        },btn)
        Corner(sideLine)

        -- tooltip
        local tip=New("TextLabel",{
            Text=tName, TextSize=12,
            TextColor3=T.T1, Font=T.FM,
            Size=UDim2.new(0,0,0,24),
            AutomaticSize=Enum.AutomaticSize.X,
            Position=UDim2.new(0,-6,0.5,0),
            AnchorPoint=Vector2.new(1,0.5),
            BackgroundColor3=T.BG4,
            BackgroundTransparency=0,
            Visible=false, ZIndex=70,
        },btn)
        Pad(tip,0,8,0,8)
        Corner(tip,UDim.new(0,6))
        Stroke(tip,T.Brd,0.84,1)
        btn.MouseEnter:Connect(function() tip.Visible=true end)
        btn.MouseLeave:Connect(function() tip.Visible=false end)

        -- scroll
        local scroll=New("ScrollingFrame",{
            Size=UDim2.new(1,0,1,0),
            BackgroundTransparency=1,
            ScrollBarThickness=3,
            ScrollBarImageColor3=T.Acc,
            ScrollBarImageTransparency=0.4,
            CanvasSize=UDim2.new(0,0,0,0),
            Visible=false, ZIndex=51,
            BorderSizePixel=0,
        },W.ContentArea)

        local cList=New("Frame",{
            Size=UDim2.new(1,0,0,0),
            AutomaticSize=Enum.AutomaticSize.Y,
            BackgroundTransparency=1, ZIndex=52,
        },scroll)
        List(cList,Enum.FillDirection.Vertical,Enum.HorizontalAlignment.Left,6)
        Pad(cList,10,12,10,12)

        local Tab={_scroll=scroll, _list=cList, _W=W, _btn=btn}

        local function Activate()
            if W._active then
                W._active._scroll.Visible=false
                local ob=W._active._btn
                Tw(ob,{BackgroundTransparency=1},.15)
                local oi=ob:FindFirstChild("Icon")
                if oi then
                    if oi:IsA("ImageLabel") then Tw(oi,{ImageColor3=T.T3},.15)
                    else Tw(oi,{TextColor3=T.T3},.15) end
                end
                local os=ob:FindFirstChildOfClass("Frame")
                if os then Tw(os,{BackgroundTransparency=1,Size=UDim2.new(0,3,0,0)},.15) end
            end
            W._active=Tab
            scroll.Visible=true
            Tw(btn,{BackgroundTransparency=0.82},.15)
            local ic=btn:FindFirstChild("Icon")
            if ic then
                if ic:IsA("ImageLabel") then Tw(ic,{ImageColor3=T.Acc2},.15)
                else Tw(ic,{TextColor3=T.Acc2},.15) end
            end
            Tw(sideLine,{BackgroundTransparency=0,Size=UDim2.new(0,3,0,22)},.2,Enum.EasingStyle.Back)
        end

        btn.Activated:Connect(Activate)
        if #W._tabs==0 then Activate() end
        table.insert(W._tabs,Tab)

        -- ─────────────────────────────────────
        --  Element builders
        -- ─────────────────────────────────────

        local function Card(h, clip)
            local f=New("Frame",{
                Size=UDim2.new(1,0,0,h or 44),
                BackgroundColor3=T.BG2,
                ZIndex=53,
                ClipsDescendants=clip or false,
            },cList)
            Corner(f)
            Stroke(f,T.Brd,0.88,1)
            return f
        end

        -- ── Label ────────────────────────────
        function Tab:Label(c)
            c=c or {}
            local f=New("Frame",{
                Size=UDim2.new(1,0,0,18),
                BackgroundTransparency=1,ZIndex=53,
            },cList)
            local l=Lbl(f,c.Text or "",10,T.T3,T.FS)
            l.Size=UDim2.new(1,0,1,0)
            l.TextSize=10
            -- optional accent line before
            if c.Accent then
                New("Frame",{
                    Size=UDim2.new(0,3,0,10),
                    Position=UDim2.new(0,-2,0.5,0),
                    AnchorPoint=Vector2.new(0,0.5),
                    BackgroundColor3=T.Acc,
                    BorderSizePixel=0,ZIndex=54,
                },f)
                Pad(f,0,0,0,6)
            end
        end

        -- ── Separator ────────────────────────
        function Tab:Separator()
            New("Frame",{
                Size=UDim2.new(1,0,0,1),
                BackgroundColor3=T.Brd,
                BackgroundTransparency=0.87,
                BorderSizePixel=0,ZIndex=53,
            },cList)
        end

        -- ── Button ───────────────────────────
        function Tab:Button(c)
            c=c or {}
            local f=Card(40)
            Pad(f,0,12,0,12)

            local btn2=New("TextButton",{
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,
                Text="",ZIndex=54,
            },f)

            -- name
            local nl=Lbl(f,c.Name or "Button",14,T.T1,T.FS)
            nl.Size=UDim2.new(1,0,0,18)
            nl.Position=UDim2.new(0,0,0.5,-9)

            if c.Desc then
                nl.Position=UDim2.new(0,0,0,7)
                local dl=Lbl(f,c.Desc,11,T.T3,T.FM)
                dl.Size=UDim2.new(1,0,0,13)
                dl.Position=UDim2.new(0,0,0,24)
            end

            -- right arrow
            local arr=Lbl(f,"›",16,T.T3,T.FB)
            arr.Size=UDim2.new(0,14,1,0)
            arr.Position=UDim2.new(1,-14,0,0)
            arr.TextXAlignment=Enum.TextXAlignment.Right

            btn2.MouseEnter:Connect(function()
                Tw(f,{BackgroundColor3=T.BG3},.12)
                Tw(arr,{TextColor3=T.Acc2},.12)
            end)
            btn2.MouseLeave:Connect(function()
                Tw(f,{BackgroundColor3=T.BG2},.12)
                Tw(arr,{TextColor3=T.T3},.12)
            end)
            btn2.MouseButton1Down:Connect(function() Tw(f,{BackgroundColor3=T.BG4},.07) end)
            btn2.MouseButton1Up:Connect(function()
                Tw(f,{BackgroundColor3=T.BG3},.1)
                if c.Callback then task.spawn(pcall,c.Callback) end
            end)
        end

        -- ── Toggle ───────────────────────────
        function Tab:Toggle(c)
            c=c or {}
            local val   = c.Default or false
            local bKey  = c.Key
            local bMode = c.KeyMode or "Toggle"
            local rec   = false

            local f=Card(44)
            Pad(f,0,12,0,12)

            -- name/desc
            local nf=New("Frame",{
                Size=UDim2.new(1,-92,1,0),
                BackgroundTransparency=1,ZIndex=54,
            },f)
            local nl=Lbl(nf,c.Name or "Toggle",14,T.T1,T.FS)
            nl.Size=UDim2.new(1,0,0,18)
            nl.Position=UDim2.new(0,0,0.5,-9)
            if c.Desc then
                nl.Position=UDim2.new(0,0,0,7)
                local dl=Lbl(nf,c.Desc,11,T.T3,T.FM)
                dl.Size=UDim2.new(1,0,0,13)
                dl.Position=UDim2.new(0,0,0,24)
            end

            -- right side
            local rf=New("Frame",{
                Size=UDim2.new(0,88,1,0),
                Position=UDim2.new(1,0,0,0),
                AnchorPoint=Vector2.new(1,0),
                BackgroundTransparency=1,ZIndex=54,
            },f)
            New("UIListLayout",{
                FillDirection=Enum.FillDirection.Horizontal,
                VerticalAlignment=Enum.VerticalAlignment.Center,
                HorizontalAlignment=Enum.HorizontalAlignment.Right,
                Padding=UDim.new(0,8),
            },rf)

            -- keybind pill
            local kpil=New("TextButton",{
                Size=UDim2.new(0,0,0,22),
                AutomaticSize=Enum.AutomaticSize.X,
                BackgroundColor3=T.BG4,
                Text=bKey and KName(bKey) or "None",
                TextSize=10,TextColor3=T.T3,Font=T.FM,
                ZIndex=55,LayoutOrder=0,
            },rf)
            Corner(kpil,UDim.new(0,5))
            local kStroke=Stroke(kpil,T.Brd,0.84,1)
            Pad(kpil,0,7,0,7)

            -- switch
            local swBg=New("Frame",{
                Size=UDim2.new(0,38,0,20),
                BackgroundColor3=T.BG4,
                ZIndex=55,LayoutOrder=1,
            },rf)
            Corner(swBg,UDim.new(0,10))
            Stroke(swBg,T.Brd,0.84,1)

            local swThumb=New("Frame",{
                Size=UDim2.new(0,14,0,14),
                Position=UDim2.new(0,3,0.5,0),
                AnchorPoint=Vector2.new(0,0.5),
                BackgroundColor3=T.T3,ZIndex=56,
            },swBg)
            Corner(swThumb,UDim.new(1,0))

            local function SetVal(v, silent)
                val=v
                if v then
                    Tw(swBg,{BackgroundColor3=T.Acc},.2)
                    Tw(swThumb,{Position=UDim2.new(0,21,0.5,0),BackgroundColor3=Color3.new(1,1,1)},.2)
                    W:_SetInd(c.Name or "Toggle",true)
                    if not silent then
                        W:Notify({Title=c.Name or "Toggle",Message="Активировано",Type="success",Duration=2.5})
                    end
                else
                    Tw(swBg,{BackgroundColor3=T.BG4},.2)
                    Tw(swThumb,{Position=UDim2.new(0,3,0.5,0),BackgroundColor3=T.T3},.2)
                    W:_SetInd(c.Name or "Toggle",false)
                    if not silent then
                        W:Notify({Title=c.Name or "Toggle",Message="Деактивировано",Type="info",Duration=2.5})
                    end
                end
                if c.Callback then task.spawn(pcall,c.Callback,v) end
            end
            SetVal(val,true)

            local clickBtn=New("TextButton",{
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,Text="",ZIndex=57,
            },f)
            clickBtn.Activated:Connect(function() SetVal(not val) end)

            -- keybind record
            kpil.Activated:Connect(function()
                rec=true
                kpil.Text="●●●"
                kpil.TextColor3=T.Amber
                kStroke.Color=T.Amber
                kStroke.Transparency=0.35
            end)
            table.insert(W._conns,UIS.InputBegan:Connect(function(inp,gpe)
                if rec and inp.UserInputType==Enum.UserInputType.Keyboard then
                    bKey=inp.KeyCode
                    kpil.Text=KName(bKey)
                    kpil.TextColor3=T.T3
                    kStroke.Color=T.Brd
                    kStroke.Transparency=0.84
                    rec=false; return
                end
                if gpe then return end
                if bKey and inp.KeyCode==bKey then
                    if bMode=="Toggle" then SetVal(not val)
                    elseif bMode=="Hold" then SetVal(true) end
                end
            end))
            if bMode=="Hold" then
                table.insert(W._conns,UIS.InputEnded:Connect(function(inp)
                    if bKey and inp.KeyCode==bKey then SetVal(false) end
                end))
            end

            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            return {
                SetValue=SetVal,
                GetValue=function() return val end,
                SetKey=function(k) bKey=k; kpil.Text=KName(k) end,
            }
        end

        -- ── Slider ───────────────────────────
        function Tab:Slider(c)
            c=c or {}
            local mn  = c.Min     or 0
            local mx  = c.Max     or 100
            local suf = c.Suffix  or ""
            local val = math.clamp(c.Default or mn, mn, mx)
            local drag= false

            local f=Card(58)
            Pad(f,8,12,8,12)

            -- header
            local hdr=New("Frame",{
                Size=UDim2.new(1,0,0,18),
                BackgroundTransparency=1,ZIndex=54,
            },f)
            local nl=Lbl(hdr,c.Name or "Slider",13,T.T1,T.FS)
            nl.Size=UDim2.new(1,-56,1,0)

            -- value badge
            local vBg=New("Frame",{
                Size=UDim2.new(0,52,0,18),
                Position=UDim2.new(1,0,0,0),
                AnchorPoint=Vector2.new(1,0),
                BackgroundColor3=T.AccD,ZIndex=54,
            },hdr)
            Corner(vBg,UDim.new(0,5))
            Stroke(vBg,T.BrdA,0.45,1)
            local vLbl=New("TextLabel",{
                Text="",TextSize=10,TextColor3=T.Acc2,
                Font=T.FB,Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,
                TextXAlignment=Enum.TextXAlignment.Center,
                ZIndex=55,
            },vBg)

            -- percent label
            local pLbl=Lbl(f,"",10,T.T3,T.FM)
            pLbl.Size=UDim2.new(0,32,0,12)
            pLbl.Position=UDim2.new(1,-32,0,8)
            pLbl.TextXAlignment=Enum.TextXAlignment.Right

            -- track bg
            local trk=New("Frame",{
                Size=UDim2.new(1,0,0,4),
                Position=UDim2.new(0,0,0,32),
                BackgroundColor3=T.BG4,ZIndex=54,
            },f)
            Corner(trk,UDim.new(1,0))
            Stroke(trk,T.Brd,0.87,1)

            local fill=New("Frame",{
                Size=UDim2.new(0,0,1,0),
                BackgroundColor3=T.Acc,ZIndex=55,
            },trk)
            New("UIGradient",{
                Color=ColorSequence.new({
                    ColorSequenceKeypoint.new(0,T.Acc),
                    ColorSequenceKeypoint.new(1,T.Acc2),
                }),Rotation=0,
            },fill)
            Corner(fill,UDim.new(1,0))

            -- thumb
            local thumb=New("Frame",{
                Size=UDim2.new(0,16,0,16),
                Position=UDim2.new(0,0,0.5,0),
                AnchorPoint=Vector2.new(0.5,0.5),
                BackgroundColor3=Color3.new(1,1,1),
                ZIndex=56,
            },trk)
            Corner(thumb,UDim.new(1,0))
            Stroke(thumb,T.BrdA,0.3,2)
            New("ImageLabel",{
                Image="rbxassetid://5028857084",
                Size=UDim2.new(0,26,0,26),
                Position=UDim2.new(0.5,0,0.5,0),
                AnchorPoint=Vector2.new(0.5,0.5),
                BackgroundTransparency=1,
                ImageColor3=T.Acc,ImageTransparency=0.5,
                ZIndex=55,
            },thumb)

            local function Update(v)
                val=math.clamp(math.floor(v+0.5),mn,mx)
                local pct=(val-mn)/(mx-mn)
                Tw(fill,{Size=UDim2.new(pct,0,1,0)},.08)
                Tw(thumb,{Position=UDim2.new(pct,0,0.5,0)},.08)
                vLbl.Text=tostring(val)..suf
                pLbl.Text=tostring(math.floor(pct*100)).."%"
                if c.Callback then task.spawn(pcall,c.Callback,val) end
            end
            Update(val)

            local function Pos2Val(x)
                local a=trk.AbsolutePosition.X
                local w=trk.AbsoluteSize.X
                return mn+math.clamp((x-a)/w,0,1)*(mx-mn)
            end

            trk.InputBegan:Connect(function(i)
                if i.UserInputType==Enum.UserInputType.MouseButton1 then
                    drag=true; Update(Pos2Val(i.Position.X))
                end
            end)
            thumb.InputBegan:Connect(function(i)
                if i.UserInputType==Enum.UserInputType.MouseButton1 then drag=true end
            end)
            UIS.InputEnded:Connect(function(i)
                if i.UserInputType==Enum.UserInputType.MouseButton1 then drag=false end
            end)
            UIS.InputChanged:Connect(function(i)
                if drag and i.UserInputType==Enum.UserInputType.MouseMovement then
                    Update(Pos2Val(i.Position.X))
                end
            end)

            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            return {SetValue=Update, GetValue=function() return val end}
        end

        -- ── Dropdown (multi-select) ───────────
        function Tab:Dropdown(c)
            c=c or {}
            local opts  = c.Options  or {}
            local multi = c.Multi    or false
            local sel   = {}
            local open  = false
            local IH    = 30
            local baseH = 44
            local maxV  = 5

            if c.Default then
                if type(c.Default)=="table" then
                    for _,v in ipairs(c.Default) do sel[v]=true end
                else sel[c.Default]=true end
            end

            local f=New("Frame",{
                Size=UDim2.new(1,0,0,baseH),
                BackgroundColor3=T.BG2,
                ClipsDescendants=true,ZIndex=53,
            },cList)
            Corner(f)
            local fStroke=Stroke(f,T.Brd,0.88,1)
            Pad(f,0,12,0,12)

            -- header
            local hdr=New("Frame",{
                Size=UDim2.new(1,0,0,44),
                BackgroundTransparency=1,ZIndex=54,
            },f)
            local nl=Lbl(hdr,c.Name or "Dropdown",13,T.T1,T.FS)
            nl.Size=UDim2.new(1,-62,1,0)

            -- count pill
            local cpil=New("Frame",{
                Size=UDim2.new(0,26,0,18),
                Position=UDim2.new(1,-30,0.5,0),
                AnchorPoint=Vector2.new(1,0.5),
                BackgroundColor3=T.AccD,ZIndex=54,
                Visible=multi,
            },hdr)
            Corner(cpil,UDim.new(0,9))
            Stroke(cpil,T.BrdA,0.45,1)
            local cLbl=New("TextLabel",{
                Text="0",TextSize=10,TextColor3=T.Acc2,Font=T.FB,
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,
                TextXAlignment=Enum.TextXAlignment.Center,
                ZIndex=55,
            },cpil)

            -- arrow
            local arw=New("TextLabel",{
                Text="▾",TextSize=11,TextColor3=T.T3,Font=T.FB,
                Size=UDim2.new(0,14,1,0),
                Position=UDim2.new(1,-14,0,0),
                AnchorPoint=Vector2.new(1,0),
                BackgroundTransparency=1,ZIndex=54,
            },hdr)

            -- separator
            New("Frame",{
                Size=UDim2.new(1,0,0,1),
                Position=UDim2.new(0,0,0,44),
                BackgroundColor3=T.Brd,
                BackgroundTransparency=0.87,
                BorderSizePixel=0,ZIndex=54,
            },f)

            -- option list
            local ol=New("Frame",{
                Size=UDim2.new(1,0,0,0),
                Position=UDim2.new(0,0,0,45),
                BackgroundTransparency=1,ZIndex=54,
            },f)
            New("UIListLayout",{
                FillDirection=Enum.FillDirection.Vertical,
                SortOrder=Enum.SortOrder.LayoutOrder,
                Padding=UDim.new(0,0),
            },ol)

            local function CountSel()
                local n=0; for _,v in pairs(sel) do if v then n=n+1 end end; return n
            end
            local function FireCb()
                if not c.Callback then return end
                if multi then
                    local t={}; for k,v in pairs(sel) do if v then t[#t+1]=k end end
                    task.spawn(pcall,c.Callback,t)
                else
                    for k,v in pairs(sel) do if v then task.spawn(pcall,c.Callback,k); return end end
                    task.spawn(pcall,c.Callback,nil)
                end
            end

            local optRefs={}
            for _,opt in ipairs(opts) do
                local item=New("TextButton",{
                    Size=UDim2.new(1,0,0,IH),
                    BackgroundColor3=T.BG3,
                    BackgroundTransparency=1,
                    Text="",ZIndex=55,
                },ol)

                local cb=New("Frame",{
                    Size=UDim2.new(0,14,0,14),
                    Position=UDim2.new(0,0,0.5,0),
                    AnchorPoint=Vector2.new(0,0.5),
                    BackgroundColor3=T.BG4,ZIndex=56,
                },item)
                Corner(cb,UDim.new(0,3))
                Stroke(cb,T.Brd,0.83,1)

                local cm=New("TextLabel",{
                    Text="✔",TextSize=9,TextColor3=Color3.new(1,1,1),Font=T.FB,
                    Size=UDim2.new(1,0,1,0),
                    BackgroundTransparency=1,
                    TextXAlignment=Enum.TextXAlignment.Center,
                    Visible=false,ZIndex=57,
                },cb)

                local ol2=Lbl(item,opt,13,T.T2,T.FM)
                ol2.Size=UDim2.new(1,-22,1,0)
                ol2.Position=UDim2.new(0,22,0,0)

                local function Upd()
                    if sel[opt] then
                        Tw(cb,{BackgroundColor3=T.Acc},.12)
                        cm.Visible=true
                        Tw(ol2,{TextColor3=T.Acc2},.12)
                    else
                        Tw(cb,{BackgroundColor3=T.BG4},.12)
                        cm.Visible=false
                        Tw(ol2,{TextColor3=T.T2},.12)
                    end
                end
                Upd()

                item.MouseEnter:Connect(function() Tw(item,{BackgroundTransparency=0.87},.1) end)
                item.MouseLeave:Connect(function() Tw(item,{BackgroundTransparency=1},.1) end)
                item.Activated:Connect(function()
                    if multi then sel[opt]=not sel[opt]
                    else for k in pairs(sel) do sel[k]=false end; sel[opt]=true end
                    Upd(); cLbl.Text=tostring(CountSel()); FireCb()
                end)
                optRefs[opt]={upd=Upd}
            end
            Pad(ol,0,0,4,0)

            local function Toggle()
                open=not open
                local th=open and (baseH+1+math.min(#opts,maxV)*IH+4) or baseH
                Tw(f,{Size=UDim2.new(1,0,0,th)},.2,Enum.EasingStyle.Quint)
                Tw(arw,{Rotation=open and 180 or 0},.2)
                fStroke.Color    = open and T.BrdA or T.Brd
                fStroke.Transparency = open and 0.45 or 0.88
            end

            local ca=New("TextButton",{
                Size=UDim2.new(1,0,0,44),
                BackgroundTransparency=1,Text="",ZIndex=57,
            },f)
            ca.Activated:Connect(Toggle)
            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            cLbl.Text=tostring(CountSel())

            return {
                GetSelected=function()
                    local t={}; for k,v in pairs(sel) do if v then t[#t+1]=k end end; return t
                end,
                SetSelected=function(list)
                    for k in pairs(sel) do sel[k]=false end
                    if type(list)=="table" then for _,v in ipairs(list) do sel[v]=true end
                    else sel[list]=true end
                    for _,r in pairs(optRefs) do r.upd() end
                    cLbl.Text=tostring(CountSel())
                end,
            }
        end

        -- ── Keybind ──────────────────────────
        function Tab:Keybind(c)
            c=c or {}
            local bKey  = c.Key  or nil
            local bMode = c.Mode or "Toggle"
            local active= false
            local rec   = false

            local f=Card(44)
            Pad(f,0,12,0,12)

            -- icon
            local iconF=New("Frame",{
                Size=UDim2.new(0,28,0,28),
                Position=UDim2.new(0,0,0.5,0),
                AnchorPoint=Vector2.new(0,0.5),
                BackgroundColor3=T.BG4,ZIndex=54,
            },f)
            Corner(iconF,UDim.new(0,7))
            Stroke(iconF,T.Brd,0.84,1)
            New("TextLabel",{
                Text="⌨",TextSize=14,TextColor3=T.T2,Font=T.FB,
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,
                TextXAlignment=Enum.TextXAlignment.Center,
                TextYAlignment=Enum.TextYAlignment.Center,
                ZIndex=55,
            },iconF)

            -- name / mode
            local nl=Lbl(f,c.Name or "Keybind",13,T.T1,T.FS)
            nl.Size=UDim2.new(1,-140,0,16)
            nl.Position=UDim2.new(0,36,0,5)

            local ml=Lbl(f,bMode:upper(),10,T.T3,T.FM)
            ml.Size=UDim2.new(1,-140,0,12)
            ml.Position=UDim2.new(0,36,0,23)

            -- key chip
            local kBtn=New("TextButton",{
                Size=UDim2.new(0,0,0,24),
                AutomaticSize=Enum.AutomaticSize.X,
                Position=UDim2.new(1,-60,0.5,0),
                AnchorPoint=Vector2.new(1,0.5),
                BackgroundColor3=T.BG4,
                Text=bKey and KName(bKey) or "None",
                TextSize=11,TextColor3=T.T2,Font=T.FM,
                ZIndex=55,
            },f)
            Corner(kBtn,UDim.new(0,5))
            local kStr=Stroke(kBtn,T.Brd,0.82,1)
            Pad(kBtn,0,8,0,8)

            -- status dot
            local sDot=New("Frame",{
                Size=UDim2.new(0,8,0,8),
                Position=UDim2.new(1,-8,0.5,0),
                AnchorPoint=Vector2.new(1,0.5),
                BackgroundColor3=T.T3,ZIndex=55,
            },f)
            Corner(sDot,UDim.new(1,0))

            local function SetActive(v)
                active=v
                if v then
                    Tw(sDot,{BackgroundColor3=T.Green},.15)
                    W:_SetInd(c.Name or "Keybind",true)
                    W:Notify({Title=c.Name or "Keybind",Message="Кейбинд активирован",Type="success",Duration=2.5})
                else
                    Tw(sDot,{BackgroundColor3=T.T3},.15)
                    W:_SetInd(c.Name or "Keybind",false)
                    W:Notify({Title=c.Name or "Keybind",Message="Кейбинд деактивирован",Type="info",Duration=2.5})
                end
                if c.Callback then task.spawn(pcall,c.Callback,v) end
            end

            kBtn.Activated:Connect(function()
                rec=true
                kBtn.Text="●●●"
                kBtn.TextColor3=T.Amber
                kStr.Color=T.Amber
                kStr.Transparency=0.3
            end)
            table.insert(W._conns,UIS.InputBegan:Connect(function(inp,gpe)
                if rec and inp.UserInputType==Enum.UserInputType.Keyboard then
                    bKey=inp.KeyCode
                    kBtn.Text=KName(bKey)
                    kBtn.TextColor3=T.T2
                    kStr.Color=T.Brd
                    kStr.Transparency=0.82
                    rec=false; return
                end
                if gpe then return end
                if bKey and inp.KeyCode==bKey then
                    if bMode=="Toggle" then SetActive(not active)
                    elseif bMode=="Hold" then SetActive(true) end
                end
            end))
            if bMode=="Hold" then
                table.insert(W._conns,UIS.InputEnded:Connect(function(inp)
                    if bKey and inp.KeyCode==bKey then SetActive(false) end
                end))
            end

            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            return {
                SetKey=function(k) bKey=k; kBtn.Text=KName(k) end,
                GetActive=function() return active end,
                SetActive=SetActive,
            }
        end

        -- ── TextInput ────────────────────────
        function Tab:Input(c)
            c=c or {}
            local f=Card(56)
            Pad(f,8,12,8,12)

            local nl=Lbl(f,c.Name or "Input",12,T.T3,T.FM)
            nl.Size=UDim2.new(1,0,0,14)

            local box=New("TextBox",{
                Size=UDim2.new(1,0,0,28),
                Position=UDim2.new(0,0,0,18),
                BackgroundColor3=T.BG3,
                TextColor3=T.T1,
                PlaceholderColor3=T.T3,
                PlaceholderText=c.Placeholder or "Введите текст...",
                Text=c.Default or "",
                TextSize=13,Font=T.FM,
                ClearTextOnFocus=false,
                ZIndex=54,
            },f)
            Corner(box,UDim.new(0,6))
            local boxStr=Stroke(box,T.Brd,0.86,1)
            Pad(box,0,8,0,8)

            box.Focused:Connect(function()
                boxStr.Color=T.BrdA
                boxStr.Transparency=0.45
            end)
            box.FocusLost:Connect(function(enter)
                boxStr.Color=T.Brd
                boxStr.Transparency=0.86
                if c.Callback then task.spawn(pcall,c.Callback,box.Text,enter) end
            end)

            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            return {
                GetValue=function() return box.Text end,
                SetValue=function(v) box.Text=v end,
            }
        end

        -- ── ColorPicker (simple) ─────────────
        function Tab:ColorPicker(c)
            c=c or {}
            local val = c.Default or Color3.fromRGB(255,100,100)
            local open= false

            local f=New("Frame",{
                Size=UDim2.new(1,0,0,44),
                BackgroundColor3=T.BG2,
                ClipsDescendants=true,ZIndex=53,
            },cList)
            Corner(f)
            Stroke(f,T.Brd,0.88,1)
            Pad(f,0,12,0,12)

            local nl=Lbl(f,c.Name or "Color",13,T.T1,T.FS)
            nl.Size=UDim2.new(1,-60,0,18)
            nl.Position=UDim2.new(0,0,0.5,-9)

            local preview=New("Frame",{
                Size=UDim2.new(0,32,0,20),
                Position=UDim2.new(1,0,0.5,0),
                AnchorPoint=Vector2.new(1,0.5),
                BackgroundColor3=val,ZIndex=54,
            },f)
            Corner(preview,UDim.new(0,6))
            Stroke(preview,T.Brd,0.82,1)

            local function SetColor(col)
                val=col; preview.BackgroundColor3=col
                if c.Callback then task.spawn(pcall,c.Callback,col) end
            end

            local ca=New("TextButton",{
                Size=UDim2.new(1,0,1,0),
                BackgroundTransparency=1,Text="",ZIndex=57,
            },f)
            ca.Activated:Connect(function()
                -- open a simple hue slider
                open=not open
                local th=open and 80 or 44
                Tw(f,{Size=UDim2.new(1,0,0,th)},.2)
                if open then
                    local hueTrack=New("Frame",{
                        Size=UDim2.new(1,0,0,14),
                        Position=UDim2.new(0,0,0,52),
                        ZIndex=54,
                    },f)
                    Corner(hueTrack,UDim.new(0,7))
                    New("UIGradient",{
                        Color=ColorSequence.new({
                            ColorSequenceKeypoint.new(0,Color3.fromHSV(0,1,1)),
                            ColorSequenceKeypoint.new(0.17,Color3.fromHSV(0.17,1,1)),
                            ColorSequenceKeypoint.new(0.33,Color3.fromHSV(0.33,1,1)),
                            ColorSequenceKeypoint.new(0.5,Color3.fromHSV(0.5,1,1)),
                            ColorSequenceKeypoint.new(0.67,Color3.fromHSV(0.67,1,1)),
                            ColorSequenceKeypoint.new(0.83,Color3.fromHSV(0.83,1,1)),
                            ColorSequenceKeypoint.new(1,Color3.fromHSV(1,1,1)),
                        }),Rotation=0,
                    },hueTrack)

                    local hDrag=false
                    local function PickHue(x)
                        local a=hueTrack.AbsolutePosition.X
                        local w=hueTrack.AbsoluteSize.X
                        local h=math.clamp((x-a)/w,0,1)
                        SetColor(Color3.fromHSV(h,1,1))
                    end
                    hueTrack.InputBegan:Connect(function(i)
                        if i.UserInputType==Enum.UserInputType.MouseButton1 then
                            hDrag=true; PickHue(i.Position.X)
                        end
                    end)
                    UIS.InputEnded:Connect(function(i)
                        if i.UserInputType==Enum.UserInputType.MouseButton1 then hDrag=false end
                    end)
                    UIS.InputChanged:Connect(function(i)
                        if hDrag and i.UserInputType==Enum.UserInputType.MouseMovement then
                            PickHue(i.Position.X)
                        end
                    end)
                end
            end)

            f.MouseEnter:Connect(function() Tw(f,{BackgroundColor3=T.BG3},.12) end)
            f.MouseLeave:Connect(function() Tw(f,{BackgroundColor3=T.BG2},.12) end)

            return {
                SetValue=SetColor,
                GetValue=function() return val end,
            }
        end

        return Tab
    end  -- AddTab

    -- ── Destroy ───────────────────────────────
    function W:Destroy()
        for _,c in ipairs(self._conns) do c:Disconnect() end
        self.Gui:Destroy()
    end

    -- ── SetTitle ──────────────────────────────
    function W:SetTitle(t)
        titleLbl.Text = t
    end

    return W
end  -- CreateWindow

return Nebula
