client.load_type_definitions()
    root = client.get_root_node()
    print("Root node is: ", root)
    objects = client.get_objects_node()
    print("Objects node is: ", objects)
    print("Children of root are: ", root.get_children())
    var = client.get_node("ns=1;s=OCTAGON.Satellites.S5-03.DataPacks.Irrigation_Queue.StationStates")
    print(var)
    handler =SubHandler()
    sub = client.create_subscription(5000, handler)
    print("OPCUA Create Subscription")
    handle = sub.subscribe_data_change(var)
    hand=sub.create_monitored_items(var)
    tempT1 = root.get_child(["0:Objects", "1:OCTAGON.Satellites.S5-03.DataPacks.Irrigation_Queue.StationStates"])
    print (tempT1)
    print(var)
    b = var.get_data_value()  # get value of node as a DataValue object
    c = var.get_value()
    print("my-var is: ", b, c)
   
    
    print(handle)

      # get value of node as a python builtin
    time.sleep(10)

except  :
    sub.unsubscribe()
    sub = client.create_subscription(5000, handler)
    print (sub)
    time.sleep(20)
