# db.userdata.find({
    $and:[{gender:"Female"},
    {age:{$ne:15}},
    {age:{$lt: 30}}
    ]
}).project({age:1,gender:1}).sort({ age:1 })

<!-- ---------         ---------------- -->
# db.userdata.find({
    $or:[{gender:"Female"},
    {"skills.name":"PYTHON"},
    {age:{$lt: 30}}
    ]
}).project({skills:1}).sort({ age:1 })