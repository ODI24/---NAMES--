function Create(base, team)
  local bb = Instance.new('BillboardGui', game.CoreGui)
  bb.Adornee = base
  bb.ExtentsOffset = Vector3.new(0,1,0)
  bb.AlwaysOnTop = true
  bb.Size = UDim2.new(0,5,0,5)
  bb.StudsOffset = Vector3.new(0,1,0)
  bb.Name = 'tracker'
  local frame = Instance.new('Frame',bb)
  frame.ZIndex = 10
  frame.BackgroundTransparency = 0.3
  frame.Size = UDim2.new(1,0,1,0)
  local txtlbl = Instance.new('TextLabel',bb)
  txtlbl.ZIndex = 10
  txtlbl.BackgroundTransparency = 1
  txtlbl.Position = UDim2.new(0,0,0,-35)
  txtlbl.Size = UDim2.new(1,0,10,0)
  txtlbl.Font = 'ArialBold'
  txtlbl.FontSize = 'Size12'
  txtlbl.Text = base.Parent.Name:upper()
  txtlbl.TextStrokeTransparency = 0.5
  if team then
      txtlbl.TextColor3 = Color3.new(0,1,1)
      frame.BackgroundColor3 = Color3.new(0,1,1)
  else
      txtlbl.TextColor3 = Color3.new(1,0,0)
      frame.BackgroundColor3 = Color3.new(1,0,0)
  end
end

function Clear()
  for _,v in pairs(game.CoreGui:children()) do
      if v.Name == 'tracker' and v:isA('BillboardGui') then
          v:Destroy()
      end
  end
end

function Find()
  Clear()
  track = true
  spawn(function()
      while wait(1) do
          if track then
              Clear()
              for _,v in pairs(game.Players:players()) do
                  if v.TeamColor ~= game.Players.LocalPlayer.TeamColor then
                      if v.Character and v.Character.Head then
                          Create(v.Character.Head, false)
                      end
                  end
              end
          end
          wait(1)
      end
  end)
end

Find()
