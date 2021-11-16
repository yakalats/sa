 local Servicos = {
	Players = game:GetService("Players"),
	UIS = game:GetService("UserInputService"),
	RunService = game:GetService("RunService"),
	
}
Preferencias = {
	
	ProximaTab = "k",
	EsconderTabs  = "j",
	
	
	BackgroundColor3 = Color3.fromRGB(38,38,38),
	BorderColor3 = Color3.fromRGB(0,200,100),
	CorTexto = Color3.fromRGB(0,200,100),

	TextSize = 11,
	
	TextScaled = false,
	
	
	Text = "",
	
	TamanhoTab = UDim2.fromScale(0.15,1),
	DistanciaY = 0,
	ComponenteTamanho = UDim2.fromScale(0.9,0.05),
	GrupoTamanho = UDim2.fromScale(0.95,0.05),
	
	
	EscondidaPos = UDim2.fromScale(0.05,-1),
	AmostraPos = UDim2.fromScale(0.05,0.25)
}


local LocalPlayer = Servicos.Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local HasPropertie
local FmouseGui = Instance.new("ScreenGui")
local TodasTabs = {}
local TabAtual = nil
local ProxTab

FmouseGui.IgnoreGuiInset = true
FmouseGui.DisplayOrder = 2500

FmouseGui.Parent = game.CoreGui

local FMouse = {
	UI = Instance.new("ImageLabel",FmouseGui),
	Enable = function(self)
		Servicos.UIS.MouseIconEnabled = false
		self.UI.Visible = true
	end,
	Disable = function(self)
		self.UI.Visible = false
		Servicos.UIS.MouseIconEnabled = true
		if mousemoveabs then
			--mousemoveabs(self.UI.AbsolutePosition.X+32,self.UI.AbsolutePosition.Y+32)
		end
	end,
	Offset = UDim2.fromOffset(0,0)
}
FMouse.UI.Size = UDim2.fromOffset(64,64) 
FMouse.UI.Image = "rbxassetid://261279988"
--FMouse.UI.Image = "http://www.roblox.com/asset/?id=5316586394"
FMouse.UI.BackgroundTransparency = 1
FMouse.UI.ZIndex = 10
FMouse.UI.Visible = false



Imagens = {
	Circle = "rbxassetid://1325878794"
}




function map(x, in_min, in_max, out_min, out_max)
	return out_min + (x - in_min)*(out_max - out_min)/(in_max - in_min)
end

function SetUIDraggable( gui,c)
	local UserInputService = Servicos.UIS

local dragging
local dragInput
local dragStart
local startPos

local function update(input)
	local delta = input.Position - dragStart
	gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
if c then
c.Position = gui.Position
end
end

gui.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = gui.Position
		
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

gui.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)
end

local function InserirAspectRatio(Object,StandardAspect)
	local ar = Instance.new("UIAspectRatioConstraint",Object)
	local function Atualizar()
		ar.AspectRatio = Object.AbsoluteSize.X/Object.AbsoluteSize.Y
	end
	if StandardAspect == true then
		Object:GetPropertyChangedSignal("AbsoluteSize"):Connect(Atualizar)
		Atualizar()
	elseif type(StandardAspect) == "number" then
		ar.AspectRatio = StandardAspect
	end
	return ar
end

local function CarregarPreferencias()
	local CanCarregar = readfile ~= nil
	if not CanCarregar then
		return
	end
	
end
HasPropertie = function(Object,Propertie)
	return pcall(function() local a=Object[Propertie] end)
end


--} END FUNCTIONS

Classes = {
	-- Basics

	Background = function()
		local Background = Instance.new("Frame")
		Background.BackgroundTransparency = 1
		return Background
	end,
	Label = function(Parent,Type)
		
		local Label = Instance.new(Type or "TextLabel")
		Label.TextSize = Preferencias.TextSize
		Label.TextScaled = Preferencias.TextScaled
		Label.TextColor3 = Preferencias.CorTexto
		
		Label.BackgroundTransparency = 1
		Label.TextXAlignment = Enum.TextXAlignment.Left
		if type(Parent) ~= "table" then
			Label.Parent = Parent
			return Label
		else
			local ui = {
				UI = Label,
				
			}
			Label.Size = UDim2.fromScale(Preferencias.ComponenteTamanho.X.Scale,Preferencias.ComponenteTamanho.Y.Scale/1.25)
			Parent:Adicionar(ui)
			setmetatable(ui,{__index = Label,__newindex= Label})
			return ui
		end
	end,
	-- Complex
	GrupoCheck = function()
		return 
		{
			Selecionada = nil,
			Adicionar = function(self,EstadoBox,id)
				local EstadoBox = EstadoBox.EstadoBox
				EstadoBox.Estado = true
				EstadoBox.Atualizar()
				EstadoBox.Mudou = function(Estado)
					
					if Estado and self.Selecionada ~= EstadoBox then
					
						local velha = self.Selecionada
						self.Selecionada = EstadoBox
						if velha then
							velha.Atualizar()
						end
						if self.Mudou then
							self.Mudou(id)
						end
					elseif Estado == false and self.Selecionada == EstadoBox then
						EstadoBox.Atualizar()
					end
				end
			end,
		}
	end,
	EstadoBox = function(Estado)
		local Back = Instance.new("ImageButton")
		local Enchimento = Instance.new("ImageLabel",Back)
		
		local TamanhoX = 0.78
		local UI = {
			Active = true,
			Estado = Estado or false,
			OnChanged = nil,
			UI = Back,
			Enchimento = Enchimento,
		}
		
		
		Back.Size = UDim2.fromScale(TamanhoX,TamanhoX)
		Back.ImageColor3 = Color3.fromRGB(0,0,0)
		Back.ImageTransparency = 0.7
		
		Back.AnchorPoint = Vector2.new(1,0.5)
		Back.BackgroundTransparency = 1
		Back.Position = UDim2.new(1,-3,0.5,0)
		Back.Image = Imagens.Circle
		
		Enchimento.ImageColor3 = Preferencias.BorderColor3
		Enchimento.BackgroundTransparency = 1
		
		Enchimento.Position = UDim2.fromScale(0.5,0.5)
		
		Enchimento.Image = Imagens.Circle
		Enchimento.Size = UDim2.fromScale(0.8,0.8)
		Enchimento.AnchorPoint = Vector2.new(0.5,0.5)
			
		UI.Atualizar = function()
			UI.Estado = not UI.Estado
			if UI.Estado then
				Enchimento:TweenSize(UDim2.fromScale(0.8,0.8),Enum.EasingDirection.InOut,Enum.EasingStyle.Sine,0.075,true)
			else
				Enchimento:TweenSize(UDim2.fromScale(0,0),Enum.EasingDirection.InOut,Enum.EasingStyle.Sine,0.075,true)
			end
			if UI.Mudou then
				UI.Mudou(UI.Estado)
			end
		end
		if not Estado then
			Enchimento.Size = UDim2.fromScale(0,0)
		end
		Back.MouseButton1Down:Connect(UI.Atualizar)
		return UI
	end,
	-- Components
	Checkbox = function(Tab,Estado)
		local Background = Classes.Background()
		local Texto = Classes.Label(Background)
		local EstadoBox = Classes.EstadoBox(Estado or false)
		local CheckBox = {
			Estado = Estado or false,
			Active = true,
			UI = Background,
			EstadoBox = EstadoBox,
			Mudou = nil,
			Titulo = Texto
		}
		
		
		Background.Size = Preferencias.ComponenteTamanho
		
		EstadoBox.UI.Parent = Background
		EstadoBox.Mudou = function(Estado)
			CheckBox.Estado = Estado
			if CheckBox.Mudou then
				CheckBox.Mudou(Estado)
			end
			
		end
		EstadoBox.UI.AnchorPoint = Vector2.new(0,0.5)
		EstadoBox.UI.Position = UDim2.fromScale(0,0.5)
		Texto.Text = "Checkbox"
		
		Texto.Size = UDim2.fromScale(0.85,1)
		Tab:Adicionar(CheckBox)
		InserirAspectRatio(EstadoBox.UI,1)
		Texto.Position = UDim2.fromScale(0.21,0)
		return CheckBox
	end,
		Slider = function(Tab)
		local Background = Instance.new("Frame")
		local Enchimento = Instance.new("TextButton",Background)
		local Seta = Instance.new("Frame",Enchimento)
		local Slider = {
			UI = Background,
			Valor = 10,
			Maximo =10,
			Intervalos = 10,
			Mudou = nil,
		}
		
		Background.BackgroundTransparency = 1
		Background.Size = Preferencias.ComponenteTamanho
			
		Enchimento.BackgroundColor3 = Color3.fromRGB(0,0,0)
		Enchimento.BackgroundTransparency = 0.7
		Enchimento.BorderColor3 = Enchimento.BackgroundColor3
		Enchimento.Size = UDim2.fromScale(1,0.35)
		Enchimento.AnchorPoint = Vector2.new(0.5,0.5)
		Enchimento.Position = UDim2.fromScale(0.5,0.5)
		Enchimento.Text = ""
		Enchimento.AutoButtonColor = false
		
		Seta.BackgroundColor3 = Preferencias.BorderColor3
		Seta.BorderColor3 = Preferencias.BackgroundColor3
		Seta.BorderSizePixel = 0
		Seta.Size = UDim2.fromScale(0.015,1.8)
		Seta.AnchorPoint = Vector2.new(0,0.5)
		Seta.Position = UDim2.fromScale(0.05,0.5)
		
		
		local TotalStepsG = {}
		Slider.Atualizar = function(y)
			local Abz =  Enchimento.AbsoluteSize
			local Abp  = Enchimento.AbsolutePosition
			local Step = (Abz.X/(Slider.Step or Slider.Maximo))/Abz.X
			local n = (math.floor((Mouse.X - Abp.X)/Abz.X/Step+0.5) *Step)
			local f = math.clamp(n ,0,1)
			local v = Slider.Maximo * f
			if f == 1 then
				v = Slider.Maximo
			end
			Slider.Valor = v
			local p = Seta.Position
			Seta.Position = UDim2.new(f,1,0.5,0)
			if p ~= Seta.Position then
				if Slider.Mudou then
					Slider.Mudou(v)
				end
			end
			FMouse.UI.Position = UDim2.fromOffset(Seta.AbsolutePosition.X+Seta.AbsoluteSize.X-32,y)
			
		end
		Slider.SetarIntervalo = function(self,Valor)
			for _,v in pairs(TotalStepsG) do
				v:Destroy()
			end
			TotalStepsG = {}
			self.Intervalos = Valor
			local n = math.clamp(self.Maximo,0,Valor)
			for i=1,n-1 do	
				local Frame = Instance.new("Frame",Enchimento)
				Frame.BackgroundTransparency = 0.65
				Frame.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Frame.BorderSizePixel = 1
				Frame.BorderColor3 = Frame.BackgroundColor3
				Frame.AnchorPoint = Vector2.new(0.5,0)
				Frame.Position = UDim2.new(1/n * i,0)
				Frame.Size = UDim2.new(0,1,1,0)
				Frame.BorderSizePixel = 0
				table.insert(TotalStepsG,Frame)
				if i*self.Maximo/n == self.Valor then
					Frame.BackgroundColor3 = Preferencias.BorderColor3
					Frame.BackgroundColor3 = Preferencias.BorderColor3
					Frame.BackgroundTransparency = 0.5
				end
				
			end
			local x = (1/self.Maximo) * self.Valor
			self.Step = n
			Seta.Position = UDim2.new(x,1,0.5,0)
		end
		Slider.SetarPadrao =function(self,Valor)
			local n = math.clamp(self.Maximo,0,self.Intervalos)
			for i,Frame in pairs(TotalStepsG) do
				if i*self.Maximo/n == Valor then
					Frame.BackgroundColor3 = Preferencias.BorderColor3
					Frame.BackgroundColor3 = Preferencias.BorderColor3
					Frame.BackgroundTransparency = 0.5
					Seta.Position = Frame.Position + UDim2.fromScale(0,0.5)
					self.Valor = Valor
					break
				end
				
			end
			
		end
		Slider.SetarMaximo = function(self,Valor)
			self.Maximo = Valor
			self.Valor = math.clamp(self.Valor,0,Valor)
			self:SetarIntervalo(self.Intervalos)
		end
		Enchimento.MouseButton1Down:Connect(function()
			FMouse:Enable(Tab)
			local mp = Servicos.UIS:GetMouseLocation()
			local y = mp.Y - 32
			local CC
			CC = Servicos.RunService.RenderStepped:Connect(function()
				Servicos.UIS.MouseIconEnabled = false
				Slider.Atualizar(y)
				if Servicos.UIS:IsMouseButtonPressed(Enum.UserInputType.MouseButton1) == false then
					Servicos.UIS.MouseIconEnabled = true
						FMouse:Disable()
					CC:Disconnect()
				end
			end)
			
		end)
		Slider:SetarMaximo(Slider.Maximo)
		Tab:Adicionar(Slider)
		return Slider
	end,
	Grupo = function(Tab)
		local Holder = Instance.new("Frame")
		local Grid=  Instance.new("UIGridLayout",Holder)
		local X = Tab.UI.AbsoluteSize.X
		local Y = Tab.UI.AbsoluteSize.Y
		local x = X*Preferencias.ComponenteTamanho.X.Scale
		local y = Y*Preferencias.ComponenteTamanho.Y.Scale
		Grid.FillDirection = Enum.FillDirection.Horizontal
		Grid.CellSize = UDim2.new(0.9,0,0,y)
		Grid.HorizontalAlignment = Enum.HorizontalAlignment.Center

		
		Holder.BackgroundColor3 = Preferencias.BackgroundColor3
		Holder.BorderColor3 = Preferencias.BorderColor3
		Holder.BorderSizePixel = 1
		Holder.Size = Preferencias.GrupoTamanho
		
		local Grupo = {
			UI = Holder,
			Adicionar = function(self,Componente)
				Componente.UI.Parent = self.UI
				self.UI.Size = UDim2.new(self.UI.Size.X.Scale,0,Preferencias.DistanciaY, Grid.AbsoluteContentSize.Y)
				Tab:AtualizarTamanho()
				
			end
		}
		Tab:Adicionar(Grupo)
		return Grupo
	end,
	Tab = function(Parent)
		local ScreenGui = Instance.new("ScreenGui",Parent)
		local FramePrincipal = Instance.new("Frame",ScreenGui)
		local Backframe = Instance.new("Frame",ScreenGui)
		local UIList = Instance.new("UIListLayout",FramePrincipal)
		local Corner = Instance.new("UICorner",Backframe)

		Corner.CornerRadius = UDim.new(0,3)

		SetUIDraggable(Backframe,FramePrincipal)
		ScreenGui.DisplayOrder = 10
		UIList.Padding = UDim.new(Preferencias.DistanciaY,0)
		UIList.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIList.SortOrder = Enum.SortOrder.LayoutOrder
		
		ScreenGui.IgnoreGuiInset = true
		ScreenGui.ResetOnSpawn = false
		Backframe.BackgroundColor3 = Preferencias.BackgroundColor3
		Backframe.BorderSizePixel = 0
		
		FramePrincipal.Size = Preferencias.TamanhoTab
		FramePrincipal.BackgroundTransparency = 1
		FramePrincipal.Position = Preferencias.EscondidaPos

		
		Backframe.BackgroundTransparency = 0
		Backframe.Position = FramePrincipal.Position
		Backframe.ZIndex = 0
		
		
		local Tab = {
			UI = ScreenGui,
			Backframe = Backframe,
			FramePrincipal = FramePrincipal,
			Componentes = {},
			Titulo = nil
		}
		Tab.Adicionar = function(self,Componente)
			Componente.UI.Parent = FramePrincipal
			table.insert(self.Componentes,Componente)
			self:AtualizarTamanho()
		end
		Tab.AtualizarTamanho = function(self)
			Backframe.Size =  UDim2.new(FramePrincipal.Size.X.Scale,0,0.02,UIList.AbsoluteContentSize.Y)
		end
		local Titulo = Classes.Label(Tab)
		Titulo.Text = "General"
		Tab.Titulo = Titulo.UI
		Classes.Separador(Tab)
		Tab.UI.Enabled = false
		table.insert(TodasTabs,Tab)
		if #TodasTabs == 1 then
			ProxTab()
		end
		return Tab
	end,
	Separador = function(Tab)
		local Background = Classes.Background()
		local Linha = Instance.new("Frame",Background)
		local Separador = {
			UI = Background
		}
		Background.Size = UDim2.fromScale(Preferencias.ComponenteTamanho.X.Scale,Preferencias.ComponenteTamanho.Y.Scale/4)
		Linha.BackgroundColor3 = Preferencias.BorderColor3
		Linha.BorderSizePixel = 0
		Linha.AnchorPoint = Vector2.new(0,0.5)
		Linha.Size = UDim2.new(1,0,0,2)
		Tab:Adicionar(Separador)
		return Separador
	end,
	Lista = function(Tab)
		local Background =  Instance.new("Frame")
		local Fundo = Instance.new("Frame",Background)
		local Grid = Instance.new("UIGridLayout",Fundo)
		local MBotao = Instance.new("TextButton",Background)
		local Selecao = Instance.new("Frame")
		
		local y = Tab.UI.AbsoluteSize.Y*Preferencias.ComponenteTamanho.Y.Scale
		local SY = UDim2.fromScale(1,1)
		
		Background.Size = UDim2.fromScale(Preferencias.ComponenteTamanho.X.Scale,Preferencias.ComponenteTamanho.Y.Scale/1.4)
		Background.BackgroundTransparency = 1

		Grid.FillDirection = Enum.FillDirection.Horizontal
		Grid.CellSize = UDim2.new(1,0,0,y/1.4)
		Grid.CellPadding = UDim2.new(0,0,0,3)
        Grid.FillDirectionMaxCells = 15
        
		
	
		Fundo.BorderColor3 = Preferencias.BorderColor3
		Fundo.BackgroundColor3 = Preferencias.BackgroundColor3
		Fundo.ClipsDescendants = true
		Fundo.ZIndex = 10
   
		MBotao.AutoButtonColor = false
		MBotao.BackgroundTransparency = 1
		MBotao.Text = "+"
		MBotao.Size = UDim2.fromScale(0.1,1)
		MBotao.AnchorPoint = Vector2.new(1,0)
		MBotao.Position = UDim2.fromScale(1,0)
		MBotao.TextColor3 = Preferencias.BorderColor3
		MBotao.TextSize = Preferencias.TextSize*0.7
		MBotao.ZIndex =16
		
		Selecao.Position = UDim2.fromScale(0.04,0.5)
		Selecao.Size = UDim2.new(0.3,0,0.3,0)
		Selecao.AnchorPoint = Vector2.new(0,0.5)
		Selecao.BackgroundColor3 = Preferencias.BorderColor3
		Selecao.BorderSizePixel = 0
		Selecao.ZIndex = 30
        Selecao.Name = "Selecao"
        Instance.new("UICorner",Selecao).CornerRadius = UDim.new(1,0)
        
		InserirAspectRatio(Selecao,1)

	
		Fundo.Size = SY
		local TF= TweenInfo.new(0.1,Enum.EasingStyle.Sine,Enum.EasingDirection.InOut,1,false,0)
		local Lista = {
			UI = Background,
			NumItems = 0,
			Items = {},
			ItemSelecionado = nil,
            MultiSelecionar = function(self,Botao,Nome)	
				if self.ItemsSelecionados then
                     self.ItemsSelecionados[Botao.Text] = not self.ItemsSelecionados[Botao.Text]
                     Botao.Selecao.Visible = not Botao.Selecao.Visible
                end
            end,
			Adicionar = function(self,Nome)
				self.NumItems = self.NumItems + 1
				local Botao = Classes.Label(Fundo,"TextButton")
				Botao.Text = Nome
				Botao.ZIndex = 2
				Botao.TextSize = Preferencias.TextSize * 0.75
				Botao.BackgroundColor3 =Fundo.BackgroundColor3
				Botao.BackgroundTransparency = 0
				Botao.BorderSizePixel = 0
				Botao.TextColor3 = Preferencias.CorTexto
				Botao.BorderColor3 = Preferencias.BorderColor3
				Botao.ZIndex = 15
				
				Botao.Size = UDim2.fromScale(1,1)
				Botao.AutoButtonColor = false
				Botao.TextXAlignment = Enum.TextXAlignment.Center
				if self.Primeiro == nil then
					self.Primeiro = Botao
                else
                	table.insert(self.Items,Botao)
				end
				
				Botao.AutoButtonColor = false
				Selecao:Clone().Parent = Botao
				Botao.Selecao.Visible = false
				
				Botao.MouseButton1Down:Connect(function()
                	if self.Primeiro ~= Botao then
                    	if self.ItemsSelecionados then
							self:MultiSelecionar(Botao,Nome)
                        else
                        	self:Selecionar(Botao)
                        end
                    end
				end)
				
				return Botao
			end,
			Selecionar = function(self,Botao)
				local vec =Botao.AbsolutePosition
				
				self.BotaoSelecionado = Botao
				self.ItemSelecionado = Botao.Text
				Selecao.Parent = Botao
				
				if self.Mudou then
					self.Mudou(Botao.Text)
				end
			end,
			Deselecionar = function(self)
				self.ItemSelecionado = ""
				self.BotaoSelecionado.BorderSizePixel = 0
				Selecao:Remove()
				if self.Mudou then
					self.Mudou(nil)
				end
			end,
            MultiplaSelecao = function(self)
            	self.ItemsSelecionados = {}
            end,
			Atualizar = function(self)
				local Estado = not self.Estado
				local R = 45
				self.Estado = Estado
				Selecao.Visible = Estado
                
               
				if Estado then
					local tamanhoY = Grid.AbsoluteContentSize.Y 
                    self.Primeiro.ZIndex = 20
                    Fundo.ZIndex = 19
                    MBotao.ZIndex = 21
					for _,v in pairs(self.Items) do
                    	v.ZIndex = 20
                       end
		
                    local laterais = math.ceil(tamanhoY/(y/1.4 * 15)+0.5)
                    if laterais < 1 then laterais = 1 end
					Fundo.Size = UDim2.new(laterais,0,0,tamanhoY/laterais)
                    Fundo.ClipsDescendants = false
                    Grid.FillDirection = Enum.FillDirection.Vertical
                    local x = 1
                     
                   
                    Grid.CellSize = UDim2.new(1/laterais,0,0,y/1.4)
				else
                	 self.Primeiro.ZIndex = 15
                	Fundo.ZIndex = 10
                    MBotao.ZIndex = 16
					for _,v in pairs(self.Items) do
                    	v.ZIndex = 15
                      end
                	Grid.CellSize = UDim2.new(1,0,0,y/1.4)
                	Grid.FillDirection = Enum.FillDirection.Horizontal
                	Fundo.ClipsDescendants = true
					R = 0
					Fundo.Size = UDim2.fromScale(1,1)
				end
				
			end,
            Limpar = function(self)
            	local Primeiro = self.Primeiro
            	Selecao.Parent = nil
                for i,c in pairs(self.Items) do
                    	c:Destroy()
                end
                self.Items = {}
                self:Atualizar()
                self:Atualizar()
            end,
			Remover = function(self,ItemNome)
				local Botao
				local BotaoN
				for i,v in pairs(self.Items) do
					if v.Text == ItemNome then
						Botao = v
						BotaoN = i
						break
					end
				end
				if Botao then
					if self.ItemSelecionado then
						if self.ItemSelecionado.Text == Botao.Text then
							self.ItemSelecionado = nil
						end
					end
					table.remove(self.Items,BotaoN)
					Botao:Destroy()
				else
					error("Item da lista não encontrado!! (" .. ItemNome .. ")")
				end
			end,
            Preencher = function(self,tabela)
				Selecao:Remove()
            	local paraRemover = self.Items
               	for _,item in pairs(self.Items) do
                	item:Destroy()
                end
				self.Items = {}
                for _,item in pairs(tabela) do
                	self:Adicionar(tostring(item))
                end
            end,
			Estado = false,
			Titulo = nil
		}
		Tab:Adicionar(Lista)
		MBotao.MouseButton1Down:Connect(function()
			Lista:Atualizar()
		end)
		Lista.Titulo = Lista:Adicionar("Lista")
		
		return Lista
	end,
	TextBox = function(Tab)
		local Back = Classes.Background()
		local Label = Classes.Label(Back)
		local Box = Instance.new("TextBox")
		Box.BorderSizePixel = 0
		Box.Size = UDim2.fromScale(0.385,0.6)
		Box.AnchorPoint = Vector2.new(1,0.5)
		Box.Position = UDim2.fromScale(1,0.5)
		Box.BackgroundColor3 = Color3.fromRGB(58,58,58)
		Box.TextColor3 = Color3.fromRGB(255,255,255)
		Box.TextScaled = true
		Box.Parent = Back
		Back.Size = Preferencias.ComponenteTamanho
		Label.Position = UDim2.fromScale(0,0.5)
		Label.TextXAlignment = Enum.TextXAlignment.Left
		Label.Text = "Textbox"
		local TBox = {
			Box = Box,
			Mudanca = nil,
			Titulo = Label,
			UI = Back,
			DeNumero = false,
			Maximo = math.huge,
			Minimo = -math.huge
		}
		Box.Text = ""
		Box:GetPropertyChangedSignal("Text"):Connect(function()
			if TBox.Text == "" then
				return
			end
			local virgula = Box.Text:find(".")
			if virgula then
				if virgula == #Box.Text then
					return
				end
			end
			local txt = Box.Text
			if TBox.DeNumero then
				local t = tonumber(txt)
			
				if t== nil then
					Box.Text = "0"
				else
					if t > TBox.Maximo then
						Box.Text = TBox.Maximo
					elseif t < TBox.Minimo then
						Box.Text = TBox.Minimo
					end
				end
			end
			if TBox.Mudanca then
				local txt = Box.Text
				TBox.Mudanca(txt)
			end
		end)
		Tab:Adicionar(TBox)
		return TBox
	end,
	Botao = function(Tab)
		local Botao = Instance.new("TextButton")
		local Back = Instance.new("Frame")
		Back.BackgroundTransparency = 1
		Back.Size = UDim2.fromScale(Preferencias.ComponenteTamanho.X.Scale,Preferencias.ComponenteTamanho.Y.Scale*1.25)
		
		Botao.Size = UDim2.fromScale(1,0.55)
		Botao.Position = UDim2.fromScale(0,0.5)
		Botao.AnchorPoint = Vector2.new(0,0.5)
		Botao.BackgroundColor3 = Preferencias.BackgroundColor3
		Botao.BorderColor3= Preferencias.BorderColor3
		Botao.TextColor3 = Preferencias.CorTexto
		Botao.Text = "Botão"
		Botao.Parent = Back
		
		local UI = {
			UI = Back,
			MouseButton1Down = Botao.MouseButton1Down
		}
		setmetatable(UI,{__index = Botao,__newindex = Botao})
		Tab:Adicionar(UI)
		return UI
	end
}
local TabAtual
local NumTabAtual =1
local MudandoTab =false
ProxTab = function()
spawn(function()
	if MudandoTab then
		return false
	end
	MudandoTab = true
	local Pos = Preferencias.AmostraPos
	if TabAtual then
		Pos = TabAtual.Backframe.Position
		TabAtual.Backframe:TweenPosition(TabAtual.Backframe.Position -  UDim2.fromScale(0,2),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.75)
	TabAtual.FramePrincipal:TweenPosition(TabAtual.Backframe.Position - UDim2.fromScale(0,2),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.75)
		wait(0.38)
		TabAtual.UI.Enabled =false
		NumTabAtual = NumTabAtual + 1
		if NumTabAtual > #TodasTabs then
			NumTabAtual = 1
		end
	end
	local Tab = TodasTabs[NumTabAtual]
	Tab.UI.Enabled = true
	Tab.Backframe:TweenPosition(Pos)
	Tab.FramePrincipal:TweenPosition(Pos)
	TabAtual = Tab
	wait(1)
	MudandoTab =false
end)
end
local TabsEscondidas = false
Mouse.KeyDown:Connect(function(Key)
	if Key == Preferencias.ProximaTab and not TabsEscondidas then
		if #TodasTabs < 2 then
			return
		end
		ProxTab()
	elseif Key == Preferencias.EsconderTabs then
		TabsEscondidas = not TabsEscondidas
		if TabsEscondidas then
			TabAtual.UI.Enabled =false 
		else
			TabAtual.UI.Enabled =true
		end
	end
end)

return Classes,Preferencias
