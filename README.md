# Real-time-GIS-Interactive-map-of-Cameroon-Geomaterials-with-Cultural-Heritage
Real-time GIS Interactive  map of Cameroon Geomaterials with Cultural Heritage


import networkx as nx
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import Patch

# Cultural heritage items per region
heritage_items = {
    "Batouri": ["Gbaya rituals", "Baka storytelling", "Sacred forests", "Bark cloth", "Drumming", "Rain rituals", "Genealogy", "Hunting tools", "Herbal gardens", "Dance masks", "Forest altars", "Palm wine rites", "Mbela flutes", "Totems", "Gathering huts"],
    "Mobilong": ["Diamond basins", "Bush camps", "Mining songs", "Spirit forests", "Bamboo huts", "Mining rites", "Fire pits", "Carvings", "River shrines", "Chieftain sites", "Spears", "Forest folklore", "Pathways", "Diamond tales", "Tree markers"],
    "Nkamouna": ["Forest paths", "Healer huts", "Medicinal bark", "Dance rituals", "Purification", "Spell chants", "Religious carvings", "Firestones", "Spirit trees", "Herbal racks", "Water pots", "Divination", "Healing stones", "Woodcraft", "Drum circles"],
    "Figuil": ["Brick kilns", "Pottery", "Mosques", "Manuscripts", "Looms", "Leatherwork", "Calligraphy", "Drums", "Earthenware", "Blacksmiths", "Grinding stones", "Brick homes", "Jewelry", "Saddles", "Trade routes"],
    "Poli": ["Doayo statues", "Trading posts", "Hair rituals", "Oil press", "War attire", "School ruins", "Pipes", "Hilltop shrines", "Ethnic altars", "Totems", "Headrests", "Cowry belts", "Meeting stones", "Story circles", "Cave art"],
    "Mayo-Darlé": ["Tin shafts", "Mining tools", "Cattle paths", "Cattle laws", "Drums", "Rock shelters", "Fire stories", "Horn instruments", "Grain pots", "Rattles", "Whips", "Wedding flutes", "Sandals", "Salt relics", "Herbal kits"],
    "Dehane": ["Mangrove altars", "Carving tools", "River masks", "Shell jewelry", "Drum chants", "Net weaving", "Water rituals", "Deity offerings", "Salt collection", "Canoes", "Forest trails", "Raft burials", "Tide tales", "Shrimp dance", "Grass mats"],
    "Limbe": ["Slave relics", "Plant specimens", "Lava stones", "Colonial ruins", "Shackles", "Ports", "Oil presses", "Museums", "Stone carvings", "Monument", "Dance troupes", "Festival drums", "Kribi tales", "Missionary sites", "Oral histories"],
    "Western Highlands": ["Foumban Palace", "Bafut Palace", "Regalia", "Royal drums", "Initiation masks", "Thrones", "Bells", "Stools", "Museums", "Calabashes", "Tablets", "Spears", "Fire pits", "Instruments", "Embroidery"]
}

regions = list(heritage_items.keys())
num_nodes = 100

# Generate random geometric graph
radius = 0.2
G = nx.random_geometric_graph(num_nodes, radius)
pos = nx.get_node_attributes(G, 'pos')

# Assign a random region to each node
np.random.seed(42)
node_regions = {node: np.random.choice(regions) for node in G.nodes()}

# Map regions to colors
colors_list = ['red', 'green', 'blue', 'orange', 'purple', 'brown', 'pink', 'cyan', 'magenta']
region_color_map = dict(zip(regions, colors_list))

# Prepare node colors
node_colors = [region_color_map[node_regions[node]] for node in G.nodes()]

# Plotting
plt.figure(figsize=(16, 10))

# Draw edges and nodes
nx.draw_networkx_edges(G, pos, alpha=0.4)
nx.draw_networkx_nodes(G, pos, node_color=node_colors, node_size=80)

plt.title(f"Random Geometric Graph with {num_nodes} Nodes Colored by Region", fontsize=16)
plt.axis('on')

# Legend handles
legend_handles = [Patch(color=color, label=region) for region, color in region_color_map.items()]
plt.legend(handles=legend_handles, title="Regions", loc='upper left', fontsize=10)

# Hide the axes to avoid overlap with text
plt.gca().set_axis_off()

# Prepare full text listing of all heritage items
text_str = ""
for region, items in heritage_items.items():
    items_list = ", ".join(items)
    text_str += f"{region}:\n{items_list}\n\n"

# Add the full text box on the right side
plt.gcf().text(0.85, 0.5, text_str, fontsize=9, va='center', ha='left',
               wrap=True, bbox=dict(facecolor='white', alpha=0.8, boxstyle='round'))

plt.tight_layout()
plt.show()

