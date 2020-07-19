
def iterate_through_players_for(name, statistic)
  game_hash.each do |team, game_data|
    game_data[:players].each do |player|
      if player[:player_name] == name
        return player[statistic]
      end
    end
  end
end

def num_points_scored(player_name)
   iterate_through_players_for(player_name, :points)
end  

def shoe_size(player_name)
  iterate_through_players_for(player_name, :shoe)
end  

def team_colors(what)
   game_hash.each do |team, game_data|
    if game_data[:team_name] == what
      return game_data[:colors]
    end
  end
end  

def team_names
  game_hash.map do |team, game_data|
    game_data[:team_name]
  end
end  

def player_numbers(team_name)
  game_hash.each do |team, game_data|
    if game_data[:team_name] == team_name
      return game_data[:players].collect do |player|
        player[:number]
      end
    end
  end
end  

def player_stats(player_name)
    statistics = [
                :number,
                :shoe,
                :points,
                :rebounds,
                :assists,
                :steals,
                :blocks,
                :slam_dunks
               ]
   stats_hash = {}
  statistics.each do |stat|
    stats_hash[stat] = iterate_through_players_for(player_name, stat)
  end

  stats_hash
  
end  

def big_shoe_rebounds
    biggest_shoe = 0
  num_rebounds = 0

  game_hash.each do |team, game_data|
    game_data[:players].each do |player|
      if player[:shoe] > biggest_shoe
        biggest_shoe = player[:shoe]
        num_rebounds = player[:rebounds]
      end
    end
  end
  num_rebounds
end  
