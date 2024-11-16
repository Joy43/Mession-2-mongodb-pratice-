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

# db.userdata.updateOne(
    {_id:ObjectId("6406ad63fc13ae5a40000069"),"education.major":"Biology"}, 
{
    $set:{
        "education.$.major":"CSE"
    }
}
)


# db.userdata.deleteOne(
    {_id:ObjectId("6406ad63fc13ae5a40000065"),}

)
# db.test.aggregate([
    // stage -1

{$group: { _id: "$address.country",
count:{$sum:1},
Name:{$push:"$ROOT"}}},
// stage -2
{
    $project: {
        "fullDoc.name":1,
        "fullDoc.email":1,
        "fullDoc.phone":1,
    }
    
}

// stage -3



// stage -4

])


# db.test.aggregate([
    // stage -1

{
    $group: {
    _id:null,
    totalSalary:{$sum: "$salary"},
    totolhigh:{$max: "$salary"},
        lowsalary:{$min: "$salary"},
        avgsalary:{$avg: "$salary"},
}
},
// stage-2
{
    $project: {
         totalSalary:1,
           lowsalary:1,
        avgsalary:1,
          totolhigh:"$totolhigh",
          rangeBetweenMaxandMin:{$subtract: ["$totolhigh","$lowsalary"]}
    }
}

])


<!-- $facet -->

# db.userdata.aggregate([
   

{
    $facet: {
        // pipeline
        "friendCount":[
            // stage-1
            {$unwind: "$friends"},
            // stage-2
            {$group: { _id: "$friends",count:{$sum:1}}}
            
            ],
            // pipleline 2
           " educationCount":[
            // stage-1
            {$unwind: "$education"},
            // stage-2
            {$group: { _id: "$education",count:{$sum: 1}}}
               
               ],
            // pipeline-3
           " skillscount":[
            //   stage-1
            {$unwind: "$skills"},
            // stage-2
            {$group: { _id: "$skills",count:{$sum:1}}}
               ]
            
    }
}


])

<!-- lookup -->
# db.orders.aggregate([
    {
        
        $lookup: {
               from: "<userdata>",
               localField: "<userId>",
               foreignField: "id",
               as: "user"
             }
    }
    
    ])

 

 
 

