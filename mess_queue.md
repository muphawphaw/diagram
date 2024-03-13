```mermaid
graph LR
   
    
  id1[ \n <i class="fa-sharp fa-solid fa-computer fa-xl" style="color: ;"></i>\n  APMS UI\n\n ]:::aoo -->|Post \n ap/operations/zones| A[Zone Create]
  id1:::bo -->|"Patch \nap/operations/zones{zone_id}"|B[Zone Name \n change]
  id1:::co -->|"Post \n ap/operations/zones{id}"|C[Zone Move]
  id1:::do -->|"Delete \n ap/operations/zones/aps:move"|D[Zone Delete]
  
  subgraph O[Operation Zone]
  
  id2[ \n \n Topic Exchange \nzone_event \n \n \n ]
  A-->|zone_create.com|id2
  B-->|zone_change_name.com|id2
  C-->|zone_move.com|id2
  D-->|zone_delete.com|id2
  subgraph Z[Zone Event]
    id2<-->|zone_delete.*|H([<i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i>\nzone delete queue])
    id2<-->|zone_move.*|G([<i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i>\nzone move queue])
    id2<-->|zone_change_name.*|F([<i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i> \nzone name change queue])
    id2<-->|zone_create.*|E([<i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i><i class="fa-regular fa-envelope fa-xl" style="padding-right:5px"></i>\nzone create queue])
  end
  id3[<i class="fa-regular fa-file fa-xl"></i>\npython]
  id4[Create zone worker]
  id5[Zone name \n change worker]
  id6[Zone move worker]
  id7[Zone delete worker]

  end

  id9[Operation zone] & id10[Profile]
  id3-->|Zone overview|id8
  id3-->|Zone info|id9
  id3-->|AP info|id10

  E --- id4 --> E
  id4 --- E
  F --- id5 --> F
  id5 --- F
  G --- id6 --> G
  id6 --- G
  H --- id7 --> H
  id7 --- H

  
  id4 & id5 & id6 & id7 -->id8

  id8[( \n \n   Redis DB    \n \n)]
    
  H-->|"view/ap/profiles/{cid}"|id11[Profile]
  H-->|ap/firmware_mapping\n /ap/command|id12[Status]
  H-->|api/v1/apms_ap|id13[OSS]
  
  classDef aoo fill:#1E90FF,stroke:#1E90FF
  class id1,id3 aoo
  classDef boo fill:#90EE90,stroke:#90EE90
  class A,E boo
  classDef coo fill:#00BFFF,stroke:#00BFFF
  class B,F coo
  classDef doo fill:#FFA500,stroke:#FFA500
  class C,G doo
  classDef eoo fill:#FF0000,stoke:#FF0000
  class D,H eoo
  style id8 fill:#DC143C
  style id2 fill:#ADD8E6,stroke:#ADD8E6
  classDef sRed stroke:red
  class id7,id11,id12,id13 sRed
  style id4 stroke:#90EE90,stroke-width: 3px
  style id5 stroke:#00BFFF,stroke-width: 3px
  style id6 stroke:#FFA500,stroke-width: 3px
  classDef astro stroke:#1E90FF,stroke-width:4px
  class id9,id10 astro


  classDef lava fill:#D3D3D3
  class O lava
  style O stroke:#D3D3D3
  classDef wheat fill:#FAF0E6,stroke:#FAF0E6
  class Z wheat

%%    style id11 stroke:#f66,stroke-dasharray: 5 5
    linkStyle 15,17,18,20,21,23,24,26 stroke:none


  linkStyle 11,16,27 stroke:#189142
  linkStyle 10,19,28 stroke:#00BFFF
  linkStyle 9,22,29 stroke:#FFA500
  linkStyle 8,25,30 stroke:#FF0000
