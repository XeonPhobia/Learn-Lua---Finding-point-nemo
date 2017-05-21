-- Find a tile that is sea
local function findSea()
  counter = counter + 1
  x, y = Random[counter], Random[100 + counter]
end

-- Find the distance to shore from a specific tile
local function distanceToShore(x, y, a)
  if map[x][y] == "#" then return 0 end
  local xa = a
  local ya = 0
  while xa >= 0 do
      if map[x+xa % 23][y+ya % 83] == "#" then return a end
      if map[x-xa % 23][y+ya % 83] == "#" then return a end
      if map[x+ya % 23][y+xa % 83] == "#" then return a end
      if map[x+ya % 23][y-xa % 83] == "#" then return a end
  xa = xa - 1
  ya = ya + 1
  end
  return   distanceToShore(x, y, a + 1);
end

-- Optimize the distance to shore from a specific tile
local function OptimizeDistanceToShore(x, y)
  here = distanceToShore(x, y, 0)
  north = distanceToShore(x-1, y, 0)
  south = distanceToShore(x+1, y, 0)
  east = distanceToShore(x, y+1, 0)
  west = distanceToShore(x, y-1, 0)
  if north > here then return OptimizeDistanceToShore(x-1, y) end  
  if south > here then return OptimizeDistanceToShore(x+1, y) end  
  if east > here then return OptimizeDistanceToShore(x, y+1) end
  if west > here then return OptimizeDistanceToShore(x, y-1) end
  return x, y;
end

-- define 2d array 'map'
map = {}
for i = 0, 24 do
  map[i] = {}
end

-- make random numbers
counter = 0
Random = {}
for i = 1, 100 do
  Random[i] = math.random(25)
  Random[100 + i] = math.random(84)
end

-- makefile array 'mapLine'
local file = io.open("map.txt", "r");
mapLine = {}
for line in file:lines() do
  table.insert(mapLine, line);
  map[line] = {}
end

-- array 'mapLine' into 2d matrix 'map'
for line = 1, #mapLine do
  for i = 1, 84 do
    map[line-1][i-1] = mapLine[line]:sub(i,i);
  end
end

resultsArray = {}
CurrentDistance = 0
CurrentX = 0
CurrentY = 0
for i = 1, 100 do
  findSea()
  newDistance = distanceToShore(x,y,0)
  if CurrentDistance < newDistance then CurrentDistance = newDistance; CurrentX = x; CurrentY = y; end
end
CurrentX, CurrentY = OptimizeDistanceToShore(CurrentX, CurrentY)
print(CurrentX, CurrentY)
